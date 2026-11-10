# bot test harness

Runs test games for a game-playing bot on GitHub Actions, one batch per manually dispatched run.

- Every batch is ciphertext (OpenPGP, AES-256), uploaded as a release asset and deleted after use. Its key is a
  one-off repository secret, deleted with the run once the result is collected.
- The key is read only inside new network, mount and PID namespaces (loopback only, a private tmpfs for every
  decrypted byte). The result is encrypted before it leaves and kept as a 1-day artifact. The log shows fixed lines.
- The workflow runs only on manual dispatch, has no token permissions and uses one GitHub action, pinned by hash.

Public metadata: when runs happen, how long they take, and the sizes of the encrypted files.
