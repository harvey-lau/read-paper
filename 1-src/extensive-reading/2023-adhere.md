# The Extensive Reading of 2023-[*AdHere: Automated Detection and Repair of Intrusive Ads*](https://ieeexplore.ieee.org/document/10172610)

- The **problem** is that little is known about how well websites comply with *Better Ads Standards* and whether existing approaches are sufficient for developers to quickly resolve such issues.
- The **solution** is AdHere, a technique that can detect intrusive ads that do not comply with **Better Ads Standards** and suggest repair proposals.

The workflow of online ad (refer to Figure 2 for more details) is:

1. Websites preallocate slots for advertisements by including bootstrapping JavaScript ad libraries provided by ad networks. When a user visits a website, these snippets are executed in the user's browser.
2. These ad libraries collect and send the user/website profiles to the real-time bidding platform.
3. User profiles are further shared with participating ad networks and advertisers before a read-time auction is conducted.
4. Advertisers evaluate its value and bid for a particular impression.
5. Additional JavaScript snippets are returned to the end user and eventually load the actual ad content (e.g., videos, images or texts) from the auction winner.

Then, what are Better Ads Standards? leading media associations and corporations conducted a study with 66,000 users to identify the least favorable ad experiences and developed the Better Ads Standards, which define 4 unacceptable desktop (D) and 8 unacceptable mobile (M) ads (refer to Figure 3 for more details). For example:

- **Pop-up Ads (D-1 and M-1)** usually appear to deliberately block the main content of a web page. They may include a forced count down that requires users to wait.
- **Ad Density Higher than 30% (M-5)** of a page are considered intrusive, where the density measured by dividing the sum of all ad heights by the total height of the main content of the page.

The workflow of AdHere includes 3 steps (refer to Figure 8 for more details):

1. **Collecting Website Status**. AdHere collects the Better Ads Standards compliance status for 1,000,000 websites each day.
2. **Pinpointing Violating Ads**. When the ad status changes from `PASSING` to `FAILING`, AdHere analyzes the pages and looks for violating ads.
3. **Suggesting Repair Proposals**. When the ad status restores from `FAILING` to `PASSING`, AdHere assumes the violations are fixed. AdHere compares the `PASSING` DOM tree with the `FAILING` DOM tree to learn fixes from developers.

> The [Document Object Model](https://en.wikipedia.org/wiki/Document_Object_Model) (DOM) is a cross-platform and language-independent interface that treats an HTML or XML document as a tree structure wherein each node is an object representing a part of the document.

The advantages of AdHere are shown in Figure 1.
