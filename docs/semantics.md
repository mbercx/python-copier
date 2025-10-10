# Semantics

> You may be sure, my dear Cebes, that inaccurate language is not only itself a mistake; it implants evil in men's souls.
> - [Socrates](https://www.jstor.org/stable/pdf/1398850.pdf)

- **Localized** code: Keep meaning and effects close to where they’re used. Prefer small, single-purpose functions, tight scopes, and minimal globals so behavior is easy to reason about and change safely.

## Acronyms

- **EAFP**: Easier to ask forgiveness than permission - write the straightforward operation and handle the specific failure (`try`/`except`) instead of pre-checking.
