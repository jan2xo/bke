---
name: bke
description: Use the GitHub connector with the BKE-approved read-only and write tool catalog. Invoke tools through the actual `GitHub` callable namespace exposed by the runtime.
---

# BKE

BKE is an instruction and policy wrapper for GitHub engineering work.

## Connector and callable namespace

Use the connected GitHub connector for all repository, issue, pull request, commit, file, branch, review, and workflow operations.

The callable tool namespace is `GitHub`.

Examples:

- `GitHub.get_repo`
- `GitHub.fetch_file`
- `GitHub.update_file`
- `GitHub.create_pull_request`
- `GitHub.fetch_commit_workflow_runs`

BKE is not itself a callable namespace, connector, MCP server, or API. Never invent or invoke `BKE.*`, `bke.*`, `@BKE.*`, or `plugin://bke...` as functions.

The catalogs below use fully qualified callable names. Treat the GitHub tools actually exposed in the current runtime as authoritative. If a cataloged callable is not exposed in the current session, do not fabricate it; report that it is unavailable.

## Write tools

`GitHub.add_comment_to_issue`, `GitHub.add_issue_assignees`, `GitHub.add_issue_labels`, `GitHub.add_reaction_to_issue_comment`, `GitHub.add_reaction_to_pr`, `GitHub.add_reaction_to_pr_review_comment`, `GitHub.add_review_to_pr`, `GitHub.convert_pull_request_to_draft`, `GitHub.create_blob`, `GitHub.create_branch`, `GitHub.create_commit`, `GitHub.create_file`, `GitHub.create_issue`, `GitHub.create_pull_request`, `GitHub.create_tree`, `GitHub.delete_file`, `GitHub.dismiss_pull_request_review`, `GitHub.enable_auto_merge`, `GitHub.label_pr`, `GitHub.lock_issue_conversation`, `GitHub.mark_pull_request_ready_for_review`, `GitHub.merge_pull_request`, `GitHub.remove_issue_assignees`, `GitHub.remove_issue_label`, `GitHub.remove_pull_request_reviewers`, `GitHub.remove_reaction_from_issue_comment`, `GitHub.remove_reaction_from_pr`, `GitHub.remove_reaction_from_pr_review_comment`, `GitHub.reply_to_review_comment`, `GitHub.request_pull_request_reviewers`, `GitHub.rerun_failed_workflow_run_jobs`, `GitHub.rerun_workflow_job`, `GitHub.resolve_review_thread`, `GitHub.unlock_issue_conversation`, `GitHub.unresolve_review_thread`, `GitHub.update_file`, `GitHub.update_issue`, `GitHub.update_issue_comment`, `GitHub.update_pull_request`, `GitHub.update_ref`, `GitHub.update_review_comment`.

## Read-only tools

`GitHub.compare_commits`, `GitHub.download_user_content`, `GitHub.download_workflow_artifact`, `GitHub.fetch`, `GitHub.fetch_blob`, `GitHub.fetch_commit`, `GitHub.fetch_commit_workflow_runs`, `GitHub.fetch_file`, `GitHub.fetch_issue`, `GitHub.fetch_issue_comments`, `GitHub.fetch_pr`, `GitHub.fetch_pr_comments`, `GitHub.fetch_pr_file_patch`, `GitHub.fetch_pr_patch`, `GitHub.fetch_workflow_job_logs`, `GitHub.fetch_workflow_job_steps`, `GitHub.fetch_workflow_run_artifacts`, `GitHub.fetch_workflow_run_jobs`, `GitHub.get_commit_combined_status`, `GitHub.get_issue_comment_reactions`, `GitHub.get_pr_diff`, `GitHub.get_pr_info`, `GitHub.get_pr_reactions`, `GitHub.get_pr_review_comment_reactions`, `GitHub.get_profile`, `GitHub.get_repo`, `GitHub.get_repo_collaborator_permission`, `GitHub.get_user_login`, `GitHub.get_users_recent_prs_in_repo`, `GitHub.list_installations`, `GitHub.list_installed_accounts`, `GitHub.list_pr_changed_filenames`, `GitHub.list_pull_request_review_threads`, `GitHub.list_pull_request_reviews`, `GitHub.list_recent_issues`, `GitHub.list_repositories`, `GitHub.list_repositories_by_affiliation`, `GitHub.list_repositories_by_installation`, `GitHub.list_user_org_memberships`, `GitHub.list_user_orgs`, `GitHub.search`, `GitHub.search_branches`, `GitHub.search_commits`, `GitHub.search_installed_repositories_streaming`, `GitHub.search_installed_repositories_v2`, `GitHub.search_issues`, `GitHub.search_prs`, `GitHub.search_repositories`.

## Operating rules

- Treat GitHub as canonical for BKE engineering work.
- Inspect current state and record the exact starting SHA before changing code.
- Use read-only `GitHub.*` callables for discovery and verification; use write `GitHub.*` callables only when the user requests a mutation.
- Prefer the smallest surgical change that satisfies the request.
- Preserve existing branches, workflows, and unrelated changes.
- Treat CI failures as evidence; patch only failures that are understood and relevant to the requested work.
- Verify the exact resulting commit, checks, and workflow state after writes.
- Never claim a write occurred unless the GitHub connector confirms it.
