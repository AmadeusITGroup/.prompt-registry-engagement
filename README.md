# Prompt Registry Engagement Data

This repository contains pre-computed engagement data (ratings and feedback) for the [Awesome Copilot Hub](https://github.com/AmadeusITGroup/prompt-registry-config).

## Files

- **`ratings.json`** - Bundle ratings computed from community feedback
- **`feedbacks.json`** - User feedback and comments for bundles

## Data Structure

### ratings.json

Contains aggregated rating data for all bundles in the hub:

```json
{
  "version": "1.0.0",
  "generated": "2026-01-29T12:00:00Z",
  "bundles": [
    {
      "sourceId": "awesome-copilot-official",
      "bundleId": "frontend-web-dev",
      "upvotes": 45,
      "downvotes": 3,
      "wilsonScore": 0.89,
      "starRating": 4.5,
      "totalVotes": 48,
      "lastUpdated": "2026-01-29T12:00:00Z",
      "confidence": "high"
    }
  ]
}
```

**Note**: The `sourceId` field is required to uniquely identify bundles across different sources.

### feedbacks.json

Contains user feedback and comments:

```json
{
  "version": "1.0.0",
  "generated": "2026-01-29T12:00:00Z",
  "bundles": [
    {
      "sourceId": "awesome-copilot-official",
      "bundleId": "frontend-web-dev",
      "feedbacks": [
        {
          "id": "feedback-1",
          "rating": 5,
          "comment": "Excellent bundle! Very helpful prompts.",
          "timestamp": "2026-01-20T10:30:00Z",
          "version": "latest"
        }
      ]
    }
  ]
}
```

## Usage

These files are referenced in the hub configuration:

```yaml
engagement:
  enabled: true
  ratings:
    enabled: true
    ratingsUrl: https://raw.githubusercontent.com/AmadeusITGroup/.prompt-registry-engagement/main/ratings.json
  feedback:
    enabled: true
    feedbackUrl: https://raw.githubusercontent.com/AmadeusITGroup/.prompt-registry-engagement/main/feedbacks.json
```

## Updating Data

The engagement data is generated from GitHub Discussions using the `compute-ratings` CLI tool from the [prompt-registry](https://github.com/AmadeusITGroup/prompt-registry) project.

### Generating Ratings

```bash
# From the prompt-registry project
npx compute-ratings \
  --config collections.yaml \
  --output ratings.json \
  --token $GITHUB_TOKEN
```

### Generating Feedbacks

```bash
# From the prompt-registry project
npx harvest-feedbacks \
  --config collections.yaml \
  --output feedbacks.json \
  --token $GITHUB_TOKEN
```

## Statistics

- **Total bundles**: 67
- **Bundles with ratings**: 67
- **Bundles with feedback**: 14
- **Last updated**: 2026-01-29
