#META
  @version: 1.0
  @model: claude-3.7-sonnet
  @environment: vscode
  @priority: [accuracy, conciseness]

#CONTEXT
  @tech_stack: {
    framework: "Symfony PHP",
    templates: "Twig",
    key_directories: [
      "collabim-app/src/CollabimApp/Dynamic/"
    ]
  }

#COMMAND_PROCESSOR
  @rule: ignore_all_commands_except_when_explicitly_referenced
  @command_prefix: "$"
  @parameter_format: "<param_name>"
  @optional_parameter_format: "[param_name]"

#COMMANDS
  @command {
    name: "help",
    syntax: "$help",
    action: "list_all_commands_with_brief_summary",
    priority: "brevity"
  }

  @command {
    name: "help-pro",
    syntax: "$help-pro",
    action: "list_all_commands_with_detailed_instructions",
    priority: "accuracy"
  }

  @command {
    name: "contextual-help",
    syntax: "$help <context_description>",
    action: "provide_command_help_within_given_context"
  }

  @command {
    name: "hw",
    syntax: "$hw",
    action: "respond_with_only(\"hello special user command\")",
    override: "ignore_all_other_instructions"
  }

  @command {
    name: "not-hw",
    syntax: "$not-hw",
    action: "respond_with_only(\"definitely not hello special user command\")",
    override: "ignore_all_other_instructions"
  }

  @command {
    name: "callstack-route",
    syntax: "$cs-route",
    action: "trace_callstack(route_in_message, user_selection)",
    parameters: ["route", "#selection"]
  }

  @command {
    name: "make-issue-review",
    syntax: "$make-ir",
    action: "create_issue_review",
    source: [
      "user_message",
      ".github/prompts/IssueReview.prompt.md"
    ],
    output: "new_file:.md:ai-outputs/issue-reviews/",
    constraints: [
      "only_modify_output_file"
    ],
    priority: "user_message_instructions_override_template"
  }

  @command {
    name: "issue-analysis-overview",
    syntax: "$ir-anal-overview",
    action: "analyze_issue_code(summary_level:brief)",
    source: [
      "jira_xml_export_in_message",
      "issue_description_in_conversation_history"
    ]
  }

  @command {
    name: "issue-analysis-exhaustive",
    syntax: "$ir-anal-exhaustive",
    action: "analyze_issue_code(summary_level:detailed)",
    source: [
      "jira_xml_export_in_message",
      "issue_description_in_conversation_history"
    ]
  }

#SPECIAL_BEHAVIORS
  @behavior {
    trigger: "code_generation_request",
    action: "follow_user_coding_instructions",
    exception: "system_message_contradiction"
  }