## What are we going to do?
___

## Why are we doing it?
___

## When are we going to do it?

* Start time: ___
* Duration: ___
* Estimated end time: ___

## How are we going to do it?
___

## How are we preparing for it?
___

## What can we check before starting?
___

## What can we check afterwards to ensure that it's working?
___

## Impact

* Type of impact: <internal|client facing|no impact>
* What will happen: ___
* Do we expect downtime? (set the override in pagerduty): ___

## How are we communicating this to our customers?

* [Announce the deployment] well in advance: ___
* Tweet after the change.

[Announce the deployment]: https://gitlab.com/gitlab-org/takeoff/blob/master/doc/announce-a-deployment.md

## What is the rollback plan?
___

## Monitoring

* Graphs to check for failures:
  * ___
* Graphs to check for improvements:
  * ___
* Alerts that may trigger:
  * ___

## [IF NEEDED]

### Google Doc to follow during the change (remember to link in the on-call log)
___

### Scheduling

Schedule a downtime in the production calendar twice as long as your worst duration estimate, be pessimistic (better safe than sorry)

### When things go wrong (downtime or service degradation)

* Label the change issue as outage
* Perform a blameless post mortem

## References

* [Making changes to GitLab.com](https://about.gitlab.com/handbook/infrastructure/#making-changes-to-gitlabcom)
* [Infrastructure links](https://about.gitlab.com/handbook/infrastructure/#common-links)
* [On-Call Log](https://docs.google.com/document/d/1nWDqjzBwzYecn9Dcl4hy1s4MLng_uMq-8yGRMxtgK6M/edit#)
* [Blameless Postmortems Guideline](https://about.gitlab.com/handbook/infrastructure/#postmortems)
* [Monitoring](http://monitor.gitlab.net)

/label ~change
