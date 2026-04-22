# GeekFon Society Cartridge

## What This Is
GeekFon Society is the LESARUSS music, radio, and podcast network layer. Plays two roles: the in-universe media label inside The Blueprint (the sitcom), and the real distribution platform for music, radio, and podcast content across the LESARUSS Universe. Waiting room on April 20 soft launch. Spelling: **GeekFon** (F-O-N), never GeekFun.

## Domain
- Primary URL: `geekfonsociety.com`
- Radio: GeekFon Radio (built, deployed inside the Huddle, live stream URL pending)
- Podcast hosting target: Captivate (captivate.fm) via API — queued for integration

## Key People
- **Jasmine Laurent** — Chief Creative Officer. Owns GeekFon Radio and podcast brand consistency.
- **Dev Anand / Sable Torres** — infrastructure + API integration owners (when Captivate ships)
- Brand GMs — each brand's show backlog managed by that brand's GM

## The Product
Four layers:
1. **Personal radio** — Sean's music through the LESARUSS platform instead of Sonos. Immediate personal use case driving urgency.
2. **Member radio** — GeekFon Radio available to all LESARUSS members. Brand immersion, familiarity with the GeekFon sound.
3. **Podcast network** — Audio distribution across shows from every LESARUSS brand. GeekFon Society is the network, each brand gets a show.
4. **Content archive / backlog** — Existing catalog from Anime3000 (~6 podcasts) + TopSpot + SAR surfaces as depth-of-experience proof. "This isn't us debuting, it's people discovering what already existed."

## Captivate Integration (queued)
Automatic push via API. Content goes out without anyone logging into Captivate manually. Research targets:
- Captivate API: publish, upload, manage shows
- Shows auto-created per brand (Anime3000 show, TopSpot show, GeekFon Society show)
- RSS feed management for Apple Podcasts, Spotify, YouTube Podcasts auto-distribution
- Webhook/trigger: new episode file lands in a folder, auto-push to Captivate

## Next Steps (ordered)
1. **Immediate:** live stream URL for GeekFon Radio (Icecast, SHOUTcast, or managed like Radio.co or Airtime Pro). Jasmine owns source confirmation.
2. **Near-term:** backlog content audit. Pull all existing Anime3000 + TopSpot podcast episodes (YouTube links + raw audio) for Captivate upload queue.
3. **Medium-term:** Captivate API integration. Drop audio file + metadata in a folder, auto-publish across all podcast platforms.
4. **Long-term:** GeekFon Radio as full LESARUSS podcast network. Each brand gets a show. GeekFon Society is the flagship.

## Overlap With Other Brands
- **The Blueprint (sitcom)** — The Blueprint is set at GeekFon Society. Fictional GeekFon (in-show) = real GeekFon (in-brand)'s showcase surface. In-show Mad Tings visit is the Season 1 episode 1 premise.
- **Shamanic Resin** — GeekFon Radio distributes Shamanic Resin releases. Anime3000 episodes pair directly.
- **Mad Tings** — GeekFon Radio distributes Mad Tings releases. Never conflate with Shamanic Resin.
- **Anime3000** — shared production stack (Seedance + Suno). Anime3000 music feeds GeekFon Radio.
- **Chester Is Cool** — Chester music videos feed GeekFon Radio + waiting room library.
- **TopSpot** — legacy podcast catalog lives on GeekFon Radio as archive show.
- **Russell's Roving Reporters** — RRR podcast segments feed GeekFon Radio as dedicated shows.
- **Vegans Explore + 111 Day Theory + SAR** — each gets a podcast show on the network.
- **LESARUSS Academy** — Academy's Creative Producer certification prepares members for podcast + radio production roles inside the GeekFon network.

## Rules
- Correct spelling: **GeekFon** (F-O-N). Never GeekFun. Universal correction rule per `feedback_geekfon_spelling.md`.
- Never conflate fictional GeekFon (inside The Blueprint sitcom) with real-brand GeekFon (this cartridge's subject) in internal docs. Same name, different layer.
- Every brand's podcast show is managed by its own GM, GeekFon Society is infrastructure, not content owner
- Music across the network feeds the shared waiting room library
- No em-dashes, ADA captions on all podcast publishes
- Members-first distribution per `console/compliance.md` Rule 4 (some podcasts ship public-first if syndicated externally; default to members-first otherwise)

## How to Apply
When any agent works on music, radio, podcast distribution, or the Captivate pipeline, load this cartridge. For in-universe sitcom context, also load `cartridges/brands/the-blueprint.md`. For music projects, also load `cartridges/brands/shamanic-resin.md` or `cartridges/brands/mad-tings.md` as relevant.
