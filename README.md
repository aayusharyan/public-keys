# Public keys

This repository holds my public cryptographic keys and my homelab’s public keys (SSH, GPG, etc.) for Git signing, server access, verification, and homelab access.

## Contents

- **keys.txt** — My personal public keys (see format below).
- **homelab-keys.txt** — Public keys for homelab machines (servers, devices, service accounts). Same format as `keys.txt`.
- Individual key files may be added for convenience (e.g. `*.pub`, `*.asc`).

## Key formats in one file

It is fine to mix key types in a single file:

- **SSH public keys** (Ed25519, RSA, ECDSA, etc.): one key per line. This matches how `authorized_keys` and most SSH tooling work.
- **GPG public keys**: ASCII-armored blocks between `-----BEGIN PGP PUBLIC KEY BLOCK-----` and `-----END PGP PUBLIC KEY BLOCK-----`. GPG tools only parse these blocks and ignore the rest of the file.

So both `keys.txt` and `homelab-keys.txt` can contain SSH lines and GPG blocks; each tool uses only the format it understands.

**Using a key file as `authorized_keys`:** You can copy or symlink `keys.txt` or `homelab-keys.txt` to `~/.ssh/authorized_keys` on a server. OpenSSH ignores lines starting with `#` and skips any line that is not a valid SSH public key (e.g. GPG block lines). Only the SSH key lines are used for authentication; comments and GPG blocks are harmless.

## Using these keys

- **My keys (keys.txt)**: Copy the SSH lines into a server’s `~/.ssh/authorized_keys` (or use the file directly as above), or use them to identify my identity (e.g. on GitHub/GitLab). For GPG: `gpg --import keys.txt`; use the fingerprint to verify my signatures or encrypt to me.
- **Homelab keys (homelab-keys.txt)**: Use for homelab SSH access (e.g. copy into `authorized_keys` on homelab hosts, or use to identify homelab machines). GPG blocks in this file can be imported the same way if present.

## Security

See [SECURITY.md](SECURITY.md) for how to report a suspected compromise or key issue.

## License

See [LICENSE](LICENSE). These keys are published for verification and encryption; use them in line with the license and common sense.
