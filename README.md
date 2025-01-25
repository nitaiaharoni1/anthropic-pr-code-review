# Anthropic Code Review Action

A composite Action that automates **pull request code reviews** using the Anthropic Claude API. This Action retrieves the git diff, sends it to Anthropic for analysis, and posts an AI-generated review as a comment on the PR.

## Features

1. **AI-driven reviews** using Anthropic’s Claude model (`claude-3-5-sonnet-20241022`).
2. Provides feedback on potential bugs, maintainability, performance, and security concerns.
3. Posts findings as a **pull request comment** in Markdown format, including:
    - Summary of changes
    - Grade (1–100)
    - Critical issues
    - Suggestions
    - Conclusion

## Usage

To use this Action, you must reference it in your GitHub workflow. Below is an example for a pull request workflow:

```yaml
name: "AI Pull Request Review"
on:
  pull_request:
    types: [ opened, synchronize, reopened ]

jobs:
  ai-code-review:
    runs-on: ubuntu-latest
    steps:
      - name: AI Code Review
        uses: your-org/anthropic-code-review-action@v1.0.0
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
```

### Step-by-Step

1. **Create a Workflow**: In your target repository, create a file at `.github/workflows/ai-review.yml`.
2. **Copy the Example**: Use the example above. Adjust the job name if desired.
3. **Add a Secret**: [Add `ANTHROPIC_API_KEY` as a repository secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets) containing your Anthropic API key.

That’s it! Whenever a pull request is opened or updated, this Action will:

1. Checkout the PR changes.
2. Generate a diff (`git diff`).
3. Submit that diff to Anthropic.
4. Post the AI’s review in the PR comments.

## Inputs

| Input               | Required | Description                                                  |
|---------------------|----------|--------------------------------------------------------------|
| `anthropic_api_key` | yes      | Your Anthropic API key (e.g., `claude-3-5-sonnet-20241022`). |

## Outputs

This Action does not currently output data for downstream steps. Instead, it posts a comment directly on the pull request.

## Limitations

- Must be triggered on pull request events (`pull_request`).
- Requires `secrets.ANTHROPIC_API_KEY` to be set.
- Usage is governed by the [LICENSE](./LICENSE).

## Support / Contact

For questions or support requests regarding this Action, please reach out to:

- **Email**: nitaiaharoni1@gmail.com
- **GitHub Issues**: [Open an issue](../../issues) if you encounter a problem using the Action.