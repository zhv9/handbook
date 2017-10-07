# GitLab QA

The manual QA testing should be done no later than 7 **working days** before
the official release.

## QA Checklist

### Login

- [ ] Regular account login
- [ ] LDAP login - _Credentials are in the **Support** 1Password vault_
- [ ] SAML login - _Credentials are in the **Support** 1Password vault, instructions are [here](saml-qa-instructions.md)_

### Forks

- [ ] Fork group project
- [ ] Push changes to fork
- [ ] Submit merge request to origin project
- [ ] Accept merge request

### Git

- [ ] Add SSH key
- [ ] Remove SSH key
- [ ] `git clone`, `git push` over SSH
- [ ] `git clone`, `git push` over HTTP with regular account
- [ ] `git clone`, `git push` over HTTP with LDAP account

### Project

- [ ] Create project
- [ ] Create project via repository import
- [ ] Transfer project to new owner
- [ ] Rename project's repository path
- [ ] Add project member
- [ ] Remove project member
- [ ] Remove project
- [ ] Create branch via UI
- [ ] Create tag via UI
- [ ] Rebase a merge request via UI, then merge the result

### Web editor

- [ ] Create a new file via UI
- [ ] Edit a file via UI
- [ ] Upload a new file via UI
- [ ] Replace a file via UI
- [ ] Remove a file via UI

### Group

- [ ] Create group
- [ ] Create project in group's namespace
- [ ] Add group member
- [ ] Remove group member
- [ ] Remove group

### Markdown

- [ ] Visit / clone [relative links repository] and see if the links are linking
  to the correct documents in the repository
- [ ] Check if images are rendered in the repository's `README`
- [ ] Click on a directory link and see if it correctly takes to the tree view
- [ ] Click on a file link and see if it correctly takes to the blob view
- [ ] Check if the links in the `README` when viewed as a blob are correct
- [ ] Select the `markdown` branch and check if all links point to the files
  within the `markdown` branch

### Syntax highlighting

- [ ] Visit/clone [language highlight repository]
- [ ] Check for obvious errors in highlighting

### Upgrader

- [ ] Upgrade from the previous release
- [ ] Run the upgrader script in this release (it should not break)

### Rake tasks

- [ ] Check if `rake gitlab:check` is updated and works
- [ ] Check if `rake gitlab:env:info` is updated and works

[relative links repository]: https://dev.gitlab.org/samples/relative-links/tree/master
[language highlight repository]: https://dev.gitlab.org/samples/languages-highlight

---

[Return to Guides](../README.md#guides)
