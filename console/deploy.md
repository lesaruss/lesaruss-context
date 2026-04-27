# Deploy Workflow — LESARUSS Universal Standard

All agents pushing code in the LESARUSS universe follow this workflow. No exceptions.

## The Golden Rule

**Never push from an unaided interactive terminal Sean has to type into.** Use one of the two supported paths.

- **Path A: Sandbox git push.** Works for multi-file batches. The sandbox proxy blocks `api.github.com` (403) but allows `github.com` HTTPS (200). `git clone` and `git push` from `/tmp` succeed. This is the default fast path for repo edits like the `lesaruss-context` repo.
- **Path B: Chrome MCP plus GitHub Contents API.** Required when the sandbox cannot reach the host or when uploading large binary files in chunks. Runs on a github.com tab via `javascript_tool`.

## Pipeline Sequence
1. Push files to GitHub via Chrome MCP javascript_tool (GitHub Contents API)
2. Run any database migrations via Supabase MCP execute_sql
3. Vercel auto-deploys on every push to main
4. Check Vercel deployment status and build logs
5. Fix any build errors and re-push

## Setup: GitHub Helper
Before pushing, set up the helper on a github.com tab. Get the tab ID from `tabs_context_mcp` first.

```javascript
window.__GH = {
  token: '<GITHUB_PAT>',
  headers: function() {
    return {
      'Authorization': 'token ' + this.token,
      'Content-Type': 'application/json',
      'Accept': 'application/vnd.github.v3+json'
    };
  }
};
```

The PAT is stored in auto-memory (`reference_github_pat.md`). Check there first.

## Small Files (under 6KB)
```javascript
(async () => {
  const path = 'path/to/file.ts';
  const url = `https://api.github.com/repos/OWNER/REPO/contents/${path}`;
  const h = window.__GH.headers();
  const res = await fetch(url, { headers: h });
  const data = await res.json();
  const sha = data.sha;
  const content = btoa(unescape(encodeURIComponent(`FILE_CONTENT_HERE`)));
  const body = { message: 'commit message', content, branch: 'main' };
  if (sha) body.sha = sha;
  const putRes = await fetch(url, { method: 'PUT', headers: h, body: JSON.stringify(body) });
  const putData = await putRes.json();
  return putData.commit ? `OK: ${putData.commit.sha.slice(0,7)}` : JSON.stringify(putData).slice(0,300);
})()
```

## Large Files (over 6KB): Chunked Transfer
Base64 encoding inflates content ~33%. Files over 6KB must be chunked to avoid Chrome MCP corruption.

**Step 1 - Encode in sandbox:**
```bash
base64 -w 0 /path/to/file.ts > /tmp/encoded.txt
```

**Step 2 - Transfer chunks to Chrome window variables (one call each):**
```javascript
window.__chunk1 = 'FIRST_6000_CHARS_OF_BASE64';
```

**Step 3 - Concatenate and push:**
```javascript
(async () => {
  const b64 = window.__chunk1 + window.__chunk2;
  delete window.__chunk1; delete window.__chunk2;
  const path = 'path/to/file.ts';
  const url = `https://api.github.com/repos/OWNER/REPO/contents/${path}`;
  const h = window.__GH.headers();
  const res = await fetch(url, { headers: h });
  const sha = res.ok ? (await res.json()).sha : undefined;
  const putRes = await fetch(url, {
    method: 'PUT', headers: h,
    body: JSON.stringify({ message: 'commit message', content: b64, sha, branch: 'main' })
  });
  const putData = await putRes.json();
  return putData.commit ? `OK: ${putData.commit.sha.slice(0,7)}` : JSON.stringify(putData).slice(0,300);
})()
```

## Critical: Chrome MCP Base64 Corruption
When pushing through Chrome MCP, base64 can corrupt files:
- `@` becomes `A` (breaks import paths like `@/lib/`)
- `const` and `for` can garble with control characters
- Regex escapes can double

**If any corruption is found: do a full file replacement. Never patch a corrupted file.**

## Supabase Migrations
Use `execute_sql` from Supabase MCP. Works for CREATE TABLE, ALTER TABLE, INSERT, and other DDL. Split large migrations into logical sections to avoid timeouts.

## Vercel Commit Author (LOCKED 2026-04-25)

Every commit pushed to a Vercel-deployed repo MUST be authored as `Sean A. Russell <contact@lesaruss.com>`. A commit authored by `claude@lesaruss.ai` triggers an instant Vercel ERROR with empty build logs because `githubCommitAuthorLogin` is missing from the deploy meta. Symptom: build queues, fails immediately, no log output.

### Sandbox git path
On every fresh clone, before the first commit:
```bash
git config user.name "Sean A. Russell"
git config user.email "contact@lesaruss.com"
```

### GitHub Contents API path
Pass `committer` and `author` in the PUT body:
```javascript
const body = {
  message: 'commit message',
  content,
  branch: 'main',
  committer: { name: 'Sean A. Russell', email: 'contact@lesaruss.com' },
  author:    { name: 'Sean A. Russell', email: 'contact@lesaruss.com' }
};
```

## Sandbox Git Push (Path A reference)

```bash
cd /tmp && git clone https://USER:TOKEN@github.com/lesaruss/REPO.git
cd REPO
git config user.name "Sean A. Russell"
git config user.email "contact@lesaruss.com"
# edit files
git add -A
git commit -m "your message"
git push origin main
```

The PAT is stored in auto-memory (`reference_github_pat.md`).

## Vercel Verification
After pushing, check deployment status:
- `list_deployments` - find the latest matching your commit SHA
- `get_deployment_build_logs` - scan for `"level": "error"` entries on failure
- States: BUILDING, READY, ERROR
- Only the most recent deployment matters. Previous ERRORs from fix attempts are noise.

## Common Build Errors
- TypeScript error: fix the code, push again
- Module not found / `A/lib/` instead of `@/lib/`: Chrome MCP base64 corruption - full file replacement
- Build worker exited with code 1: check error lines above it

## Async IIFE Requirement
All javascript_tool calls with await must use async IIFE:
```javascript
(async () => {
  // your code
  return result;
})()
```
Forgetting this causes: `SyntaxError: await is only valid in async functions`

## Repo Names
- LESARUSS Platform: `lesaruss/lesaruss-project`
- LESARUSS Context (The Signal): `lesaruss/lesaruss-context`
- BCPS Minutes: `lesaruss/bcps-minutes`
