# Laravel Legacy Version 5.2 (Extra Features)
- Some parts are already discussed on the previous sections
- Installing a package cviebrock/eloquent-sluggable by `composer require cviebrock/eloquent-sluggable`
- `cviebrock/eloquent-sluggable` turns every URL into a slug, making the URL easy to read for humans
- Pulling an avatar on Gravatar,
    - On the course, every request must be on `https://www.gravatar.com/avatar/` endpoint
    - The next part is MD5 hashing the user's email address, with the whitespace removed
    - The new (since 1/11/2024 since this file was written), all the user's email needs both leading and trailing whitespaces characters to be trimmed, force all characters to use lowercase and hash with SHA256.
    - Complete endpoint `https://www.gravatar.com/avatar/$hash`
    - [Documentation URL](https://docs.gravatar.com/general/hash/)
