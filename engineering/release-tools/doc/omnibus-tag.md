# Pushing a new omnibus tag version

There are times when it may be easier to bump the omnibus version than
releasing a new patch release. For example, let's suppose the following tags
exist in omnibus-gitlab:

* `8.15.4+ce.0`
* `8.15.4+ee.0`

If you made a mistake in the omnibus-gitlab repository (e.g. forgetting to
merge a patch in the `8-15-stable` branch), you may not want the trouble of
releasing `8.15.5` just to handle this. Instead, you can manually bump the
omnibus version to `8.15.4+ce.1` and `8.15.4+ee.1`. Follow the instructions in
the [omnibus release
documentation](https://docs.gitlab.com/omnibus/release/README.html).

Remember to include the `.1` when deploying the latest version!

---

[Return to Guides](../README.md#guides)
