# template-pnpm-typescript-monorepo

## Highlights

- changesets
- GitHub issue templates
- GitHub quality and release workflows
- pnpm workspace monorepo
- biome
- Top-level build, reset, biome, test, typecheck, and release scripts.
- Typescript

## Initial Configuration

### GitHub Repository

- [ ] Set up [trusted publishing](https://docs.npmjs.com/trusted-publishers) on npmjs for the repository.
- [ ] Configure the repository's action **Workflow Permissions** to **Read and write permissions** and to **Allow GitHub Actions to create and approve pull requests** for the changesets action.
- [ ] Set a GitHub personal access token as a GitHub secret with key `GH_PAT` to automate changeset pull requests via
  release workflow. The token should have access to "**Read** access to metadata" and "**Read** and **Write** access to code and pull requests" on the repository for the changesets action to maintain release pull requests.

### Project Files

#### `.changeset` directory

##### `config.json`

- Update `changelog` settings, including `repo`.

#### `.github` directory

##### `composite-actions/install/action.yml`

- [ ] Update `Setup Git User` command email and name

##### `ISSUE_TEMPLATE` directory

- [ ] Update `config.yml` with repository discussions link

For each template:

- [ ] Update package `options`

##### `workflows` directory

**`quality.yml`**

- Runs on branch `main` for any push or pull request.
- Runs biome and TypeScript type checks.

**`release.yml`**
> [!CAUTION]
> - Requires [trusted publishing](https://docs.npmjs.com/trusted-publishers) to be set up on npmjs to publish packages.
> - Requires a GitHub personal access token to be set in repository secrets as `GH_PAT` to automate changeset pull
    requests.

- Runs on branch `main` for any pushes that contain changes in `.changeset` or `packages`.
- Builds and publishes packages if there is a changeset version, otherwise releases changes to the `dev` tag.

- [ ] Update repository in if statement to your repo

#### `packages/_template` directory

##### `package.json`

- [ ] Update `name`
- [ ] Update `description`
- [ ] Update `author`
- [ ] Update `repository.url` and `repository.directory`
- [ ] Remove `private` if publishing to registry
- [ ] If npm registry is public, update `publishConfig`