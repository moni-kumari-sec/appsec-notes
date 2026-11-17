# Lab: Unprotected admin functionality

- **Platform:** PortSwigger Web Security Academy (Apprentice)
- **Topic:** Access control, vertical privilege escalation (BFLA)
- **Date:** 2026-11-17
- **Scope:** PortSwigger's own lab instance, which exists to be tested. No other systems.

## Summary

The lab has an admin panel that any visitor can open. There is no login check and no role check. The only protection is that the path is not linked from the site.

## Steps

1. Requested `/robots.txt`. A `Disallow` line named the admin path.
2. Requested `/administrator-panel`. It loaded for an unauthenticated visitor and listed users.
3. Used the Delete link for user `carlos`. The request was `GET /administrator-panel/delete?username=carlos`. The server answered `302` back to the panel and the user was deleted.

## Why it worked

The server did not check who was asking. It treated "the URL is not linked" as protection. `robots.txt` also advertised the path to anyone who read it.

## Missing check

Only an authenticated user with the admin role may view or call anything under `/administrator-panel`. The server must decide this on every request.

## Fix

- Deny by default: require authentication for all routes unless explicitly marked public.
- Add a role or policy check on the admin routes (in ASP.NET Core, `[Authorize(Roles = "Admin")]` or a named policy).
- Make the delete action `POST` or `DELETE` with an anti-forgery token, not a plain `GET` link.
- Do not list sensitive paths in `robots.txt`.

## Bypass variants I would test on a real fix

- Same route with a different HTTP method
- Different casing or a trailing slash (`/Administrator-Panel/`)
- Logged in as a normal user instead of anonymous
- Expired or malformed session cookie

## How I would find it without hints

`/robots.txt`, `/sitemap.xml` (this lab had none), page source and scripts, Burp site map, then common-path wordlists.

## Interview line

"The admin panel had no server-side authorization. It was hidden, not protected. The fix is a deny-by-default policy with a role check on every admin route, and sensitive actions that change state should not be plain GET requests."
