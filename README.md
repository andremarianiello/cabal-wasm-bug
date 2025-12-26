# Set up GHC WASM Meta (steps from https://www.haskell.org/ghcup/guide/#ghc-wasm-cross-bindists-experimental)
```sh
git clone https://gitlab.haskell.org/ghc/ghc-wasm-meta.git
cd ghc-wasm-meta/
export SKIP_GHC=yes
./setup.sh
source ~/.ghc-wasm/env
```
# Install GHC WASM from ghcup (steps from https://www.haskell.org/ghcup/guide/#ghc-wasm-cross-bindists-experimental)
```sh
ghcup config add-release-channel cross
ghcup install ghc --set wasm32-wasi-9.12.2.20250327 -- --host=x86_64-linux --with-intree-gmp --with-system-libffi
```

# Set up this repo (contents from https://github.com/dmjio/miso?tab=readme-ov-file#-web-assembly)

```sh
git clone <this repo>
cd <repo dir>
```

# Build repo successfully
```sh
ghcup set cabal 3.14.2.0
cabal build
```

# Fail to build repo successfully
```sh
ghcup set cabal 3.16.0.0
cabal build
```

Output:
```
Cloning into '/root/cabal-wasm-bug/dist-newstyle/src/miso-7fdae9da4bdb552ef2daf21700284a28ca9d60f6abf96b737c89243d4bad27dc'...
remote: Enumerating objects: 194, done.
remote: Counting objects: 100% (194/194), done.
remote: Compressing objects: 100% (164/164), done.
remote: Total 194 (delta 26), reused 93 (delta 6), pack-reused 0 (from 0)
Receiving objects: 100% (194/194), 266.10 KiB | 5.91 MiB/s, done.
Resolving deltas: 100% (26/26), done.
From https://github.com/dmjio/miso
 * branch            2e8dd81f9731229f83cac6137843ec3a9d498b86 -> FETCH_HEAD
HEAD is now at 2e8dd81 Reset `components` global state on hydration failure. (#1299)
Error: [Cabal-4000]
Version mismatch between ghc and ghc-pkg: /root/.ghcup/bin/wasm32-wasi-ghc is version 9.12.2.20250327 /root/.ghcup/bin/ghc-pkg is version 9.6.7
```

Note: `9.6.7` is the version of my current native, x64 GHC version. Cabal-3.16.0.0 is trying to use a different `ghc-pkg` binary than the one I specified in `cabal.project`.
