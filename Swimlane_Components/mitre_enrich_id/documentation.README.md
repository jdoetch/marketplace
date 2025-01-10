This Swimlane component translates MITRE Tactic IDs into corresponding attack phases for integration into Swimlane's SOC solution. By mapping tactics to their relevant attack phases, it enhances threat analysis and incident management workflows. The component also retrieves and returns detailed information about the associated MITRE techniques, providing context and actionable insights to SOC teams.

**Usage:**
- Create a new playbook or add the component to an existing flow
- Input tactic ID into the component’s only input “MITRE ID”, eg. “T1547.003"
- The component will look up the data and return the associated attack ID’s information
- The “mitre-attack-techniques” field may be mapped directly to SOC solution, if desired