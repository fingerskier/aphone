# aphone
An AI-English dialect built on priors.

Plain English, sharpened by sigils you've already seen elsewhere: @mentions, hashtags, shell variables, YAML, code. Each sigil has one reading, and plain English is always valid aphone.


## Definition

A simple prompt can instigate a conversation using this terse dialect. It is also the whole spec: if a model can't pick up aphone from this block alone, the dialect has grown too big.

```text
Let's talk in aphone: terse English plus sigils borrowed from code.
Plain English is always valid; sigils only sharpen it.

@x        that thing (file, person, tool)
#x        tag
$x        variable
~x        roughly / in the style of
!x        not
x?        unknown: ask or flag
a.b       b of a
k: v      parameter (this request)
a = b     bind (persists)
a -> b    into / then
a + b     and
a | b     or
(x)       qualifier
{x}       slot to fill
"x" `x`   verbatim
<t>…</t>  block
indent    sub-item

Attached sigils hug their word (#tag, !new-deps, x?); infix ones take spaces (a -> b).
Sigils inside quotes, backticks, or blocks are inert. When in doubt, it's English.
Reply in kind: aphone for structure, prose where nuance needs it.
Don't over-sigil. Write x? instead of guessing.

Example: review @src/auth.ts -> issues + fixes (security first) !style-nits
```

Every sigil at work across code, writing, planning, data, and agent hand-offs: [example.md](example.md).


## Tooling

Because attached sigils hug their word and infix sigils take spaces, usage is detectable with one regex. It's a detector, not a validator:

```
(?<!\w)(?:[@#~!][\w./-]+|\$[A-Za-z_]\w*)|\{\w+\}|\s(?:->|\||\+)\s
```

It catches attached sigils, `{slots}`, and spaced `->`, `|`, `+`; hits per word gives a rough aphone density. `$voice` counts, `$5` doesn't. `a.b`, `k: v`, `x?` and `(x)` look too much like ordinary English to count.
