## Create MR to prepare release

1. Create preparation MRs and branches for CE & EE.
```
# For release candidates use `X.Y.0-rcZ` and `X.Y.0-rcZ-ee`
bundle exec rake "patch_merge_request[X.Y.Z]"
bundle exec rake "patch_merge_request[X.Y.Z-ee]"
```

1. Update both generated merge requests:
  1. Update the pick into stable comment replacing `MERGE_REQUEST_ID` with the newly created MR's iid.
  1. `/cc` other release managers and trainees in a comment
1. Use steps in the MR descriptions to begin picking changes

## Merge CE stable changes to EE

There are a few approaches to doing the CE->EE merge: CE `X-Y-stable-patch-Z` can be merged into the existing EE preparation MR, can be merged into a new MR to fix conflicts, or could even be merged into stable.

Keeping the stable branches clean can help if you unexpectedly need to do a security release on those branches. Beyond that the trade-offs are complexity, checking pipelines are green on the branch vs MR, and creating a workflow which allows you to do things quickly and in parallel.

### To merge CE into the EE MR

1. Check out an up to date  `X-Y-stable-ee-patch-Z` branch in your local EE repo, or pull changes.
```
git fetch origin
git checkout -b X-Y-stable-ee-patch-Z origin/X-Y-stable-ee-patch-Z
```

1. Fetch `X-Y-stable-patch-Z` branch from CE ready for merging
```
git fetch git@gitlab.com:gitlab-org/gitlab-ce.git X-Y-stable-patch-Z
```

1. Merge that branch into the current EE preparation branch
```
git merge FETCH_HEAD
```

1. Optional: repeat previous two steps with `X-Y-stable` to double check that no new changes have been introduced outside of the CE preparation MR.

1. Optional: Create a new branch if you'd like to fix conflicts in a separate MR

1. Fix simple conflicts and push
```
git push origin X-Y-stable-ee-patch-Z
```

1. Optional: Ask others to help fix conflicts in the MR.

## Merging preparation MRs into stable

1. Check that no commits have been added to stable
1. Consider doing a fast-forward merge manually from the shell. The main benefit is that the HEAD commit from the MR will be the same for `X-Y-stable`, allowing you save time waiting for pipelines to turn green.
1. When pipelines are green for `X-Y-stable` and `X-Y-stable-ee`, move on to tagging the release.
