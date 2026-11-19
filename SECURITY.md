# Security

## Reporting a problem
If you think you have found a security problem in cardvault, report it through GitHub's private
vulnerability reporting here (**Security**, then **Report a vulnerability**). That is the only
way to report one; no email address is published. Please don't describe it in a public place,
such as an issue.

You will get a reply acknowledging the report. The problem is assessed, and a fix ships as a
normal signed update.

## Checking a release
Each release carries `build-record.json`, which names the commit, the tools and the hash of
every file, and `.sha256` files listing the files' SHA-256. Both are signed with the
build-record minisign key, whose public half is:

```
RWR9svcRZrJHE6qWmHKyrIBkWUMN/pga60Wt2KFv/erMPS5RbJAhGq45
```

Its key ID is `1347B26611F7B27D`. To check a release, download all its files into one folder,
install [minisign](https://jedisct1.github.io/minisign/), and run there:

```
minisign -V -P RWR9svcRZrJHE6qWmHKyrIBkWUMN/pga60Wt2KFv/erMPS5RbJAhGq45 -m SHA256SUMS.sha256
minisign -V -P RWR9svcRZrJHE6qWmHKyrIBkWUMN/pga60Wt2KFv/erMPS5RbJAhGq45 -m build-record.json
sha256sum -c SHA256SUMS.sha256
```

Each `minisign -V` prints `Signature and comment signature verified` and a trusted comment naming
the version's tag and the file; `sha256sum -c` prints `OK` for every file. Anything else means
the files are not the ones published: do not run them, and report it as above. cardvault itself
checks each update against a separate key built into the app (`latest.json.sig`).
