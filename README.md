This is my personal website.

## Local preview

1. Install Ruby + Bundler.
   On macOS, avoid the system Ruby (`/usr/bin/ruby`) for native gem builds.
   Install a user-managed Ruby first (for example with Homebrew):

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
```

2. From the repo root, run:

```bash
./bin/serve
```

Then open `http://127.0.0.1:4000`.

## One-off build

```bash
BUNDLE_PATH=vendor/bundle bundle check || BUNDLE_PATH=vendor/bundle bundle install
BUNDLE_PATH=vendor/bundle bundle exec jekyll build
```
