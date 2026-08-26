---
name: bke
description: Use the connected GitHub App with the BKE-approved read-only and write tool catalog, while treating BKE as a policy wrapper rather than a callable namespace.
---

# BKE

BKE is an instruction and policy wrapper for GitHub engineering work.

It is not a callable tool namespace, connector, MCP server, or API. Do not invent or invoke `BKE.*`, `bke.*`, `@BKE.*`, or `plugin://bke...` as functions.

When this skill is active, use the connected GitHub tool namespace that is actually exposed in the current runtime for repository, issue, pull request, commit, file, branch, review, and workflow operations.

## Tool routing

- The catalogs below describe BKE-approved GitHub operations; they are not functions owned by a `BKE` namespace.
- Treat the runtime's exposed GitHub tools as authoritative for what can actually be invoked in the current session.
- Invoke cataloged operations through the underlying GitHub tool namespace actually exposed by the runtime.
- Never translate a catalog entry into `BKE.<function>`, `bke.<function>`, or any other invented namespace.
- If a cataloged operation is not exposed by the current GitHub runtime, do not fabricate it; report that it is unavailable in the current session.

## Write tools

`add_comment_to_issue`, `add_issue_assignees`, `add_issue_labels`, `add_reaction_to_issue_comment`, `add_reaction_to_pr`, `add_reaction_to_pr_review_comment`, `add_review_to_pr`, `convert_pull_request_to_draft`, `create_blob`, `create_branch`, `create_check_run`, `create_commit`, `create_file`, `create_issue`, `create_pull_request`, `create_tree`, `delete_file`, `dismiss_pull_request_review`, `enable_auto_merge`, `label_pr`, `lock_issue_conversation`, `mark_pull_request_ready_for_review`, `merge_pull_request`, `remove_issue_assignees`, `remove_issue_label`, `remove_pull_request_reviewers`, `remove_reaction_from_issue_comment`, `remove_reaction_from_pr`, `remove_reaction_from_pr_review_comment`, `reply_to_review_comment`, `request_pull_request_reviewers`, `rerun_failed_workflow_run_jobs`, `rerun_workflow_job`, `resolve_review_thread`, `unlock_issue_conversation`, `unresolve_review_thread`, `update_check_run`, `update_file`, `update_issue`, `update_issue_comment`, `update_pull_request`, `update_ref`, `update_review_comment`.

## Read-only tools

`check_repo_initialized`, `compare_commits`, `download_git_tree_archive`, `download_user_content`, `download_workflow_artifact`, `fetch`, `fetch_blob`, `fetch_commit`, `fetch_commit_workflow_runs`, `fetch_file`, `fetch_git_blob`, `fetch_issue`, `fetch_issue_comments`, `fetch_pr`, `fetch_pr_comments`, `fetch_pr_file_patch`, `fetch_pr_patch`, `fetch_workflow_job_logs`, `fetch_workflow_job_steps`, `fetch_workflow_run_artifacts`, `fetch_workflow_run_jobs`, `get_check_run`, `get_commit_combined_status`, `get_commit_diff`, `get_commit_tree_sha`, `get_issue_comment_reactions`, `get_latest_check_run`, `get_pr_diff`, `get_pr_info`, `get_pr_reactions`, `get_pr_review_comment_reactions`, `get_profile`, `get_repo`, `get_repo_collaborator_permission`, `get_repo_installation_id`, `get_user_login`, `get_users_recent_prs_in_repo`, `list_commits`, `list_directory`, `list_git_tree`, `list_git_tree_recursive`, `list_installations`, `list_installed_accounts`, `list_pr_changed_filenames`, `list_pull_request_review_threads`, `list_pull_request_reviews`, `list_recent_issues`, `list_repositories`, `list_repositories_by_affiliation`, `list_repositories_by_installation`, `list_user_org_memberships`, `list_user_orgs`, `resolve_ref`, `search`, `search_branches`, `search_commits`, `search_installed_repositories_streaming`, `search_installed_repositories_v2`, `search_issues`, `search_prs`, `search_repositories`.

## Operating rules

- Treat GitHub as canonical for BKE engineering work.
- Inspect current state and record the exact starting SHA before changing code.
- Use read-only GitHub tools for discovery and verification; use write tools only when the user requests a mutation.
- Prefer the smallest surgical change that satisfies the request.
- Preserve existing branches, workflows, and unrelated changes.
- Treat CI failures as evidence; patch only failures that are understood and relevant to the requested work.
- Verify the exact resulting commit, checks, and workflow state after writes.
- Never claim a write occurred unless the underlying GitHub tool confirms it.
