Main release issue: <%= main_release_issue_url %>

### Summary

This MR prepares `<%= stable_branch %>` for %"<%= milestone %>" (`<%= patch_or_rc_version %>`) by merging `<%= preparation_branch_name %>` into `<%= stable_branch %>`.

### MR Filter for ~"Pick into Stable" MRs

https://gitlab.com/gitlab-org/gitlab-<%= repo_ce_or_ee %>/merge_requests?label_name%5B%5D=Pick+into+Stable&milestone_title=<%= milestone %>&scope=all&sort=updated_asc&state=merged

### MR Filter for ~"Pick into Backports" MRs

As well as picking merge requests explicitly marked for this release, you'll need to check those which need to be included in backports. Some ~"Pick into Backports" MRs won't be relevant for this release, or will have already been included; because of this you'll need to read the discussion on each MR below to decide if to include them:

https://gitlab.com/gitlab-org/gitlab-<%= repo_ce_or_ee %>/merge_requests?label_name%5B%5D=Pick+into+Backports&scope=all&sort=updated_asc&state=merged

### Note to leave in MRs

```
Picked into https://gitlab.com/gitlab-org/gitlab-<%= repo_ce_or_ee %>/merge_requests/MERGE_REQUEST_ID, will merge into `<%= stable_branch %>` ready for `<%= full_patch_or_rc_version %>`

/unlabel ~"Pick into Stable"
```

### Steps

1. Cherry-pick commits into this MR using the links for ~"Pick into Stable" and ~"Pick into Backports" above.
  - This can be done by checking out `<%= preparation_branch_name %>` locally and using `git cherry-pick -m1 MERGE_COMMIT_SHA`
1. Push changes every so often and verify that the MR has been included
1. Leave a note in the MR so others can easily see that it is on track to be included in a release.
  - If the MR no longer needs to be cherry-picked into further releases, remove the ~"Pick into Stable" label.
  - Otherwise update the milestone to the highest release it needs to be picked into, and set ~"Pick into Backports" if it needs to be picked into other releases in addition to that one.
1. If there are any conflicts while picking MRs then attempt to resolve them; otherwise, create a new MR against the `<%= preparation_branch_name %>` branch and assign it to the author of the conflicting files.
1. Merge CE-to-EE using one of the workflows described in the [Merge CE stable changes to EE docs](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/picking-into-merge-requests.md#merge-ce-stable-changes-to-ee)
1. Once this MR is green merge it to stable, preferably with a manual fast-forward merge to minimize waiting time, as described in [Merging preparation MRs into stable](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/picking-into-merge-requests.md#merging-preparation-mrs-into-stable)

### Checklist

- [ ] Changes marked ~"Pick into Stable" have been picked
- [ ] Changes marked ~"Pick into Backports" have been picked
<% if ee? %>- [ ] CE->EE merge has taken place<% end %>
- [ ] Conflicts resolved
- [ ] No new commits have introduced directly to the stable branch while this MR was in progress. If there are,<% unless ee? %> ensure these are merged into EE and<% end %> check for a green pipeline after merging this MR.
