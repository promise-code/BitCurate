# BitCurate

## Decentralized Content Curation on Bitcoin via Stacks

## Overview

**BitCurate** is a Bitcoin-native protocol for community-driven content curation built on the [Stacks blockchain](https://www.stacks.co/). It enables decentralized discovery, appraisal, and incentivization of high-quality internet content through a transparent reputation and reward system.

Built entirely in Clarity, BitCurate uses smart contracts to allow users to:

- Submit and categorize valuable online content
- Vote (upvote/downvote) on submitted items
- Earn reputation based on contribution quality
- Reward originators with STX
- Flag problematic or inappropriate submissions

All protocol activity is verifiable and transparently logged on-chain.

## Core Features

### Content Submission

Users can submit links to external content (e.g., articles, videos) with a relevant topic tag and headline. A small STX fee is required to discourage spam.

```clarity
(contribute-item "Headline" "https://example.com" "Technology")
```

### Community Appraisals

Participants can appraise (upvote/downvote) submissions. Each vote impacts:

- The content's visibility
- The voter’s credibility score

```clarity
(appraise-item item-id 1) ;; Upvote
(appraise-item item-id -1) ;; Downvote
```

### STX Gratuities

Supporters may send STX rewards directly to content originators to incentivize quality contributions.

```clarity
(reward-originator item-id amount)
```

### Content Flagging

Content can be flagged by users (except the originator) to signal potential issues (e.g., spam, misinformation).

```clarity
(flag-item item-id)
```

### Reputation System

Every user has a **credibility score** reflecting their participation and the quality of their appraisals.

## Protocol Architecture

### Smart Contracts: Written in [Clarity](https://docs.stacks.co/concepts/clarity/overview)

- **Transparent Logic**: All protocol rules are visible and immutable.
- **No Gas Fees**: Clarity is non-Turing complete, secure, and predictable.
- **Bitcoin-Secured**: Via Stacks, all interactions are anchored to Bitcoin blocks.

### Storage Maps

- `curated-items`: Stores content metadata and state
- `participant-appraisals`: Tracks user voting per item
- `participant-credibility`: Maintains user reputation
- `content-topics`: Predefined list of content categories

## Access Control

| Function                     | Access Level      |
|-----------------------------|-------------------|
| `adjust-submission-charge`  | Admin-only        |
| `introduce-topic`           | Admin-only        |
| `expunge-item`              | Admin-only        |
| Content submission/voting   | Open to everyone  |

> Admin actions require the caller to match the `PROTOCOL_ADMINISTRATOR`.

## Example Interactions

```clarity
;; Submit a new content item
(contribute-item "Decentralized Storage on IPFS" "https://ipfs.tech/" "Technology")

;; Upvote content
(appraise-item u1 1)

;; Reward the content originator
(reward-originator u1 u50)

;; Flag questionable content
(flag-item u2)

;; Retrieve content details
(retrieve-item-details u1)
```

## Query Functions

| Function                             | Description |
|--------------------------------------|-------------|
| `retrieve-item-details`             | Get metadata of a content item |
| `retrieve-participant-appraisal`    | Get a user's vote on an item |
| `retrieve-aggregate-submissions`    | Total number of submissions |
| `retrieve-participant-credibility`  | View user reputation score |
| `retrieve-top-items`                | Fetch top content by appraisal score |

## Configuration

### Constants

- `submission-charge`: Initial fee required to submit content (default: `u10`)
- `content-topics`: Up to 10 active content categories (modifiable by admin)
- `MAX_UINT`: Used for overflow checks

### Error Codes

| Code         | Meaning                       |
|--------------|-------------------------------|
| `u100`       | Unauthorized access           |
| `u101`       | Invalid content submission    |
| `u102`       | Duplicate content             |
| `u103`       | Item does not exist           |
| `u104`       | Insufficient STX balance      |
| `u105`       | Invalid or full topic list    |
| `u106`       | Invalid flag action           |
| `u107`       | Arithmetic overflow           |
| `u108`       | Invalid appraisal input       |
| `u109`       | Invalid item identifier       |

## Roadmap

- [ ] NFT badges for top contributors
- [ ] DAO-based governance for protocol changes
- [ ] Trust score decay over time
- [ ] Topic-based curation incentives

---

## Contributing

We welcome contributions, proposals, and community discussions. Feel free to fork, build, and iterate.

-

## Join the Conversation

- [Stacks Forum](https://forum.stacks.org)

**BitCurate** – Reclaim the internet’s signal.  
Curate. Appraise. Reward. Repeat.
