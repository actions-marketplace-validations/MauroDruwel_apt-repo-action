Certainly! Here’s a cleaner version of your documentation for hosting your own APT repo on GitHub:

---

# Host Your Own APT Repo on GitHub

This GitHub Action sets up and manages a simple APT repository on GitHub Pages or a separate repository.

## Inputs

### `github_token`

**Required**: Personal access token with `commit` and `push` scopes.

### `repo_supported_arch`

**Required**: Newline-delimited list of supported architectures (e.g., `amd64`, `i386`).

### `repo_supported_version`

**Required**: Newline-delimited list of supported Linux distributions (e.g., `bionic`, `trusty`).

### `file`

**Required**: Path to the `.deb` file to be included.

### `file_target_version`

**Required**: Version target for the supplied `.deb` file.

### `private_key`

**Required**: GPG private key for signing the APT repo.

### `public_key`

**Required**: GPG public key for the APT repo.

### `key_passphrase`

Passphrase for the GPG private key.

### `target_repository`

**Required**: Repository where the APT repo will be pushed (e.g., `username/apt-repo`).

### `repo_folder`

Location of the APT repo folder relative to the root of the target repository. Defaults to `repo`.

## Example Usage

```yaml
uses: jrandiny/apt-repo-action@v1
with:
  github_token: ${{ secrets.PAT }}
  repo_supported_arch: |
    amd64
    i386
  repo_supported_version: |
    bionic
    trusty
  file: my_program_bionic.deb
  file_target_version: bionic
  public_key: ${{ secrets.PUBLIC }}
  private_key: ${{ secrets.PRIVATE }}
  key_passphrase: ${{ secrets.SECRET }}
  target_repository: ${{ secrets.TARGETREPOSITORY }}
```

## Adding the APT Repository

Once the action has run and your APT repository is set up, you can add it to your system with the following commands:

```bash
wget https://YOURGITHUBPAGESURL/public.key -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://YOURGITHUBPAGESURL/repo/ bionic main"
```

Replace `YOURGITHUBPAGESURL` with your GitHub Pages URL or repository URL, and adjust the distribution and component as necessary.

--- 

Feel free to modify the instructions according to your specific setup or requirements!
