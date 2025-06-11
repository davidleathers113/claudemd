Dynamic Arguments with $ARGUMENTS
One of the most powerful features is the use of $ARGUMENTS in custom slash commands. This allows for incredibly flexible automation:
markdown# .claude/commands/fix-github-issue.md
Please analyze and fix the GitHub issue: $ARGUMENTS. Follow these steps:
1. Use `gh issue view` to get the issue details
2. Understand the problem described in the issue
3. Search the codebase for relevant files
4. Implement the necessary changes to fix the issue
5. Write and run tests to verify the fix
6. Ensure code passes linting and type checking
7. Create a descriptive commit message
8. Push and create a PR
Then you can use it like: /project:fix-github-issue 1234