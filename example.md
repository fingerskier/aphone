# aphone examples

Every sigil, in several contexts. Each scene shows the aphone, then how it reads in plain English. The legend is in the [README](README.md).


## By sigil

| sigil | code | writing | planning |
|---|---|---|---|
| `@x` | `@src/auth.ts` | `@chapter3` | `@sam` |
| `#x` | `#bug` | `#cut` | `#blocked` |
| `$x` | `build for $target` | `in $voice` | `under $budget` |
| `a = b` | `$target = node20` | `$voice = dry, wry` | `$budget = 2k/mo` |
| `k: v` | `lang: ts` | `len: 300w` | `due: fri` |
| `a.b` | `@user.email` | `@chapter3.ending` | `@launch.date` |
| `a -> b` | `@log -> root cause` | `@notes -> outline` | `ideas -> top 3` |
| `a + b` | `tests + docs` | `tighten + retitle` | `@sam + @ana` |
| `a \| b` | `fix \| flag` | `trim \| cut` | `tue \| wed` |
| `a; b` | `lang: ts; !any` | `len: 300w; !emoji` | `due: fri; owner?` |
| `~x` | `~O(n)` | `~Didion` | `~2 wks` |
| `!x` | `!@tests` | `!adverbs` | `!weekends` |
| `x?` | `node-version?` | `audience?` | `owner?` |
| `(x)` | `(if CI green)` | `(keep the joke)` | `(after launch)` |
| `[x]` | `[lint + test] -> CI` | `[intro + outro] ~Didion` | `[tue \| wed] (pm)` |
| `{x}` | `GET /{endpoint}` | `Dear {name},` | `book {venue}` |
| `"x"` `` `x` `` | `` `--force` `` | `"Ship it."` | `"no meetings"` |
| `<t>…</t>` | `<log>…</log>` | `<draft>…</draft>` | `<notes>…</notes>` |
| indent | sub-steps | sub-points | sub-tasks |


## Code review

```text
review @src/auth.ts -> issues + fixes (security first) !style-nits
```

**Reads:** Review src/auth.ts. Give me issues and fixes, security first. Skip style nits.

### …and the reply

```text
#security @src/auth.ts:42 token.exp never checked -> compare to now()
#security session secret hardcoded -> env var $SESSION_SECRET
#bug logout clears cookie !server-session -> delete that row too
/login rate-limited?
```

**Reads:** Security: line 42 never checks the token's expiry; compare it to now(). Security: the session secret is hardcoded; move it to an env var. Bug: logout clears the cookie but not the server session; delete that row too. Open question: is /login rate-limited?


## Debugging

```text
<log>
TypeError: Cannot read properties of undefined (reading 'id')
    at getUser (src/users.ts:41)
</log>
@log -> root cause + minimal patch
!@tests !new-deps
```

**Reads:** Here's a stack trace. Find the root cause and a minimal patch. Don't touch the tests or add dependencies. (The parentheses inside the log are just log; blocks are inert.)


## Writing, across turns

```text
$voice = ~Didion, dry, short sentences
rewrite @README.intro ($voice) ~120w
```

*Later in the conversation:*

```text
rewrite @CONTRIBUTING.md ($voice) !emoji
```

**Reads:** Define a voice: Didion-ish, dry, short sentences. Rewrite the README intro in that voice, about 120 words. Later: rewrite CONTRIBUTING.md in the same voice, no emoji.


## Editing

```text
<draft>
Our platform leverages cutting-edge synergies to help teams ship faster.
</draft>
@draft -> plain English ~12w | cut it (if nothing survives)
keep "ship faster" !buzzwords
```

**Reads:** Rewrite this draft in plain English, about 12 words, or cut it if nothing is left. Keep the words "ship faster" exactly. No buzzwords.


## Templates

```text
draft email to {name}
  subject: invoice 30 days late
  tone: firm + polite
  len: ~80w
  sign-off: "Best, the billing team"
```

**Reads:** Draft an email with the recipient left as a blank to fill in. Subject: invoice 30 days late. Firm but polite, about 80 words. Sign off with exactly "Best, the billing team".


## Planning

```text
#launch plan, due: oct 30
  copy + screenshots -> @ana
  pricing page -> @sam (after legal signs off)
    tiers: [2 | 3]?
  !weekend-deploys
@launch.owner?
```

**Reads:** Launch plan, due October 30. Ana takes copy and screenshots. Sam takes the pricing page once legal signs off; two tiers or three is still open. No weekend deploys. Who owns the launch?


## Data

```text
@sales.csv -> monthly revenue by region (2025 only)
  chart: bar, sort: desc
  ~0 growth -> #watch
fiscal-year-start?
```

**Reads:** From sales.csv, chart 2025 monthly revenue by region as bars, sorted descending. Tag regions with roughly flat growth "watch". When does the fiscal year start?


## Agent hand-off

```text
<ctx>
The orders endpoint paginates by offset; p95 is 2.4s at page 400.
</ctx>
@perf-agent: @api/orders.ts -> cursor pagination
  keep response shape `{ items, next }`
  !breaking-changes (v1 clients still live)
  report: diff + p95 before/after
```

**Reads:** Context: the orders endpoint pages by offset and p95 hits 2.4s at page 400. Perf agent: move api/orders.ts to cursor pagination. Keep the response shape exactly as written. No breaking changes; v1 clients are still live. Report back with the diff and p95 before and after.


## Grouping

Operators bind as in code, tight to loose: attached sigils, `.`, `+`, `|`, `->`, `=` `:`, `;`. Brackets override.

```text
review @src/auth.ts -> issues + fixes
tests + [@notes -> outline]
[@sam | @ana] + @lee
tiers: [2 | 3]?
tiers: 2 | 3?
len: ~300w; tone: dry; !emoji
```

**Reads:** Line by line. Review auth.ts into issues and fixes: `+` binds before `->`, so no bracket is needed. Write tests, and turn the notes into an outline: without the bracket it would read "turn tests and notes into an outline". Lee, plus one of Sam or Ana: without the bracket `+` binds first, giving "Sam, or Ana-and-Lee". Two tiers or three, undecided. Two tiers, or maybe three. Three settings on one line.


## Too much

```text
@me -> #want + $thing (~soon!) | ?
```

If it needs a decoder ring, write English: *"I want the thing, roughly soon, or tell me why not."*
