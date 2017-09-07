## Overview

## Threshold


### Minimum Notification

Under *minimum notification*, some changes must be proactively communicated
before they can be approved.  This can easily be addressed by providing a
few `@mentions` in the PR discussion.

Why?  This provides an *opportunity* for multiple experts (besides the
original author) to raise a red-flag if a crazy idea is being pushed
through.

### Minimum Diversity

Under *minimum diversity*, more than one person must sign-off on a PR.  This
reduces the risk of bias by incorporating an outside perspective.

Depending on the Threshold, the minimum diversity requirement may mean:

 * __Author!=Reviewer__: The review must be done by someone other than the original author.
 * __Author!=Authority__: The authority must be provided by someone other than the original author.
 * __3x__: At least three people (including the author) must indicate support for the PR.

### Minimum Authority

Under *minimum authority*, someone with recognized experience/authority in a
PR must sign-off on a PR.  This ensures that someone with instutional
knowledge (regarding various design-goals/use-cases/edge-cases) signs

The range of *possible* topics is longer than the list of commissioned
developers.

## Examples

Let's suppose:

 * Alice is "CiviContribute Principal".
 * Bob is a "Comprehensive Specialist" and also a Merger.
 * Carol is another "CiviContribute Fellow".

Now:

 * Suppose Alice proposes a Drop-in Change (DIC) to CiviContribute. Bob reviews and agrees with merging the PR. Should he merge it?
    * The requirement for "Minimum Notification" is not-applicable. So yes.
    * The requirement for "Minimum Authority" specifies "Specialist". This is met by either  Bob's authority ("Comprehensive Specialist") or Alice's authority ("CiviContribute Principal"). So yes.
    * The requirement for "Minimum Diversity" specifies "Author!=Reviewer". This is met by Bob's involvement. So yes.
    * Conclusion: yes
 * Suppose Alice proposes a Minor Change (MNC) to CiviContribute and she `@mentions` Bob and Carol. Bob reviews, agrees, and waits a couple days in case Carol has feedback. Should he merge it?
    * The requirement for "Minimum Notification" specifies two `@mentions`. This was met. So yes.
    * The requirement for "Minimum Authority" specifies "Fellow". This cannot be met by Bob's authority ("Comprehensive Specialist"), but it could be met by Alice's authority ("CiviContribute Principal"). So yes.
    * The requirement for "Minimum Diversity" specifies "Author!=Reviewer". This is met by Bob's involvement. So yes.
    * The requirement for "Minimum Diversity" specifies "Author!=Authority". The only sufficient authority came from the author (Alice), so **no**.
    * Conclusion: no
    * However...  there are a couple ways to get it approved.  Either (a) they can wait for Carol to give positive feedback or (b) Alice
      can invoke her authority as a "Principal" and document special circumstances justifying an exception.  (Ex: "This fixes a critical
      regression, and we need to get it in before RC, but Carol is on vacation.")

### Dispute Resolution

If there are multiple parties in a review, and if there is no consensus on
the acceptability of a change, then they may request resolution from a more
senior expert.
