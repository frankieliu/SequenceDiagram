# Complete SVG Sequence Diagram DSL Syntax Reference

## 🎯 **METADATA COMMANDS**
```
title <text>              # Set diagram title
theme <theme_name>        # Set visual theme (see available themes below)
terminators <type>        # Set terminator style for agent lifeline endings
headers <type>            # Set header style for first agent begin statement
autolabel <pattern>       # Set auto-labeling pattern (see patterns below)
autolabel off             # Disable auto-labeling
```

### 🎨 **Available Themes:**
```
theme basic               # Default clean theme (Helvetica/Arial fonts)
theme monospace           # Code-style theme (Courier New monospace fonts)
theme chunky              # Bold theme (thick strokes, larger elements)
theme sketch              # Hand-drawn theme (Handlee font, right-handed style)
theme "sketch left handed" # Hand-drawn theme (left-handed drawing style)
```

**Theme Details:**
- **basic** - Professional, clean appearance with standard fonts (DEFAULT)
- **monospace** - Programming/terminal style with fixed-width fonts
- **chunky** - Bold, comic-book style with thick lines and rounded elements
- **sketch** - Informal, whiteboard style with hand-drawn appearance
- **sketch left handed** - Same as sketch but mirrored for left-handed drawing

### 🔚 **Terminator & Header Types:**
```
# Valid values for both terminators and headers (5 types total):
none                      # No visual terminator/header
box                       # Rectangular box shape
bar                       # Horizontal bar
cross                     # X-shaped mark
fade                      # Gradient fade effect
```

**Usage & Defaults:**
- **terminators** - Controls visual style at END of agent lifelines (default: `none`)
- **headers** - Controls visual style at START of first agent begin (default: `box`)

**Examples:**
```
terminators cross         # End agents with X marks
headers fade             # Start first agents with fade effect
terminators none         # Clean endings (default)
headers box              # Standard box headers (default)
```

## 👥 **AGENT MANAGEMENT**
```
# Agent Creation & Control
begin <agents>                    # Create agents with box terminators
define <agents>                   # Define agent aliases/ordering
define <name> as <alias>          # Create agent with specific alias
relabel                           # Redraw agent headers in long diagrams
relabel <agents>                  # Relabel specific agents
activate <agents>                 # Show activation indicator
deactivate <agents>               # Hide activation indicator
end <agents>                      # End agents with terminator

# Agent Types
<Agent> is a <type>               # Set agent type (article optional)
<Agent> is an <type>
<Agent> is <type1> <type2>        # Multiple types
```

## 🔄 **BLOCK STRUCTURES**
```
# Conditional Blocks
if <condition>
  # statements
else if <condition>
  # statements
else
  # statements
end

# Loop Blocks
repeat <condition>
  # statements
end

# Grouping Blocks
group <label>
  # statements
end

# Reference Blocks
begin reference: <name> as <alias>
begin reference over <agents>: <name> as <alias>
```

## ➡️ **ARROW/CONNECTION TYPES**

### Base Arrow Components:
```
Line Types:     -    --    ~        (solid, dashed, wave)
Left Terms:     <    <<    ~         (arrow, double, fade)
Right Terms:    >    >>    ~    x    (arrow, double, fade, lost)
```

### Common Arrow Examples:
```
->    -->    ~>     # Basic arrows (solid, dashed, wave)
<-    <--    <~     # Reverse arrows
<->   <-->   <~>    # Bidirectional arrows
-x    --x    ~x     # Lost message indicators
<<->  ~-~    <->>   # Complex combinations
```

### Agent Flags (inline modifiers):
```
+Agent         # Activate agent
-Agent         # Deactivate agent
*Agent         # Create agent inline
!Agent         # End agent inline
+*Agent        # Create and activate
-!Agent        # Deactivate and end
```

## 📝 **CONNECTIONS & LABELS**
```
# Basic Connections
Agent1 -> Agent2                    # Simple connection
Agent1 -> Agent2: "label"           # With label (quotes recommended)
Agent1 -> Agent2: "multi\nline"     # Multiline label (quotes REQUIRED)

# ⚠️ IMPORTANT: For multiline labels, quotes are REQUIRED
Agent1 -> Agent2: "Line 1\nLine 2"  # ✅ Works - renders with line break
Agent1 -> Agent2: Line 1\nLine 2    # ❌ ERROR - renders literally

# Delayed/Asynchronous Connections
Agent1 -> ...tagname               # Start delayed connection
...tagname -> Agent2: "label"      # Complete delayed connection

# Edge Connections
[ -> Agent: "label"                # From left edge
[ <- Agent: "label"                # To left edge
Agent -> ]: "label"                # To right edge
Agent <- ]: "label"                # From right edge
```

## 📖 **NOTES, TEXT & STATE**
```
# Notes (quotes recommended, REQUIRED for multiline)
note over Agent: "text"                      # Note spanning agent
note left of Agent: "text"                   # Note to left (with "of")
note left Agent: "text"                      # Note to left (without "of")
note right of Agent: "text"                  # Note to right (with "of")
note right Agent: "text"                     # Note to right (without "of")
note between Agent1, Agent2: "text"          # Note between 2+ agents

# Multiline notes (quotes REQUIRED)
note over Agent: "Line 1\nLine 2\nLine 3"   # ✅ Works - renders with line breaks
note over Agent: Line 1\nLine 2             # ❌ ERROR - renders literally

# Text Blocks
text left of Agent: "text"                   # Left-positioned text
text right of Agent: "text"                  # Right-positioned text

# State Indicators (single agent only)
state over Agent: "text"                     # State (quotes recommended)
state over Agent: "Multi\nLine\nState"      # Multiline state (quotes REQUIRED)
```

## ➖ **DIVIDERS**
```
divider                                  # Default line (height: 6)
divider line                             # Explicit line
divider space                            # Space divider
divider delay                            # Delay divider (height: 30)
divider tear                             # Tear divider

# With Custom Heights & Labels
divider with height 40                   # Custom height
divider delay with height 50             # Delay with height
divider tear with height 20: Label      # Tear with height and label
divider: Label text                      # Any divider with label
```

## ⚡ **PARALLEL & ASYNC EXECUTION**
```
simultaneously:                         # Return to top (parallel action)
simultaneously with marker_name:        # Return to named marker
& <command>                             # Execute in parallel

marker_name:                            # Define named marker (ends with :)
```

## 🎨 **TEXT FORMATTING (Markdown)**
```
# Text Styles
*text* or _text_                        # Italic
**text** or __text__                    # Bold
~text~                                  # Strikethrough
`text`                                  # Monospace/code

# HTML Tags
<i>text</i>        <b>text</b>         # Italic, Bold
<s>text</s>        <u>text</u>         # Strikethrough, Underline
<o>text</o>                            # Overline
<sup>text</sup>    <sub>text</sub>     # Super/subscript
<red>text</red>                        # Colored text
<mark>text</mark>  <highlight>text</highlight>  # Highlighted

# Links
[text](url)                            # Markdown link
[text](url "title")                    # Link with title
<http://example.com>                   # Direct URL
```

## 🏷️ **AUTO-LABELING PATTERNS**
```
# Pattern Tokens
<label>                                # Actual message label
<inc>                                  # Auto-increment (starts at 1)
<inc 5>                               # Start at 5
<inc 1,2>                             # Start at 1, increment by 2
<inc 01>                              # Leading zeros: 01, 02, 03...
<inc 1.0>                             # Decimals: 1.0, 2.0, 3.0...

# Examples
autolabel "[<inc>] <label>"           # → "[1] message", "[2] message"
autolabel "<label> - <inc>"           # → "message - 1", "message - 2"
autolabel "<inc>"                     # → "1", "2", "3"
```

## 📋 **STRING & QUOTING RULES** ⚠️

**CRITICAL:** Escape sequences like `\n` only work inside quoted strings!

```
# ✅ CORRECT - Escape sequences work in quoted strings:
Agent -> Agent: "word\nbreak"              # Renders with line break
note over Agent: "line 1\nline 2"         # Multi-line note
title "Multi\nLine\nTitle"                 # Multi-line title

# ❌ INCORRECT - Escape sequences DON'T work in unquoted text:
Agent -> Agent: word\nbreak                # Renders literally as "word\nbreak"
note over Agent: line 1\nline 2           # Renders as "line 1\nline 2"

# 🏆 BEST PRACTICE: Always use quotes for reliable text handling
Agent -> Agent: "Simple message"           # Consistent and safe
Agent -> Agent: "Message with \"quotes\""  # Escape internal quotes with \"
```

### Quoting Rules:
```
# These are equivalent for simple text:
title "My title here"
title My title here
title My "title" here

# But for escape sequences, ONLY quoted strings work:
title "Line 1\nLine 2"          # ✅ Creates multi-line title
title Line 1\nLine 2            # ❌ Literal text "Line 1\nLine 2"
```

### String Handling Details:
- **Double quotes (")** recognized, **single quotes (') NOT** recognized
- **Quotes required for:** multiline text, escape sequences, special chars, boundary spaces
- **Escape sequences in quotes:** `\\` (backslash), `\"` (quote), `\n` (newline)
- **Control characters** (`\x00-\x1F`) are stripped everywhere
- **Recommendation:** Use quotes for all text to ensure consistent behavior

### Examples by Context:
```
# Agent names - quotes recommended for consistency
"User Interface" -> "Database": "Query data"
UI -> DB: "Simple query"                    # Works but quotes safer

# Notes and text - quotes required for multiline
note over UI: "Step 1: Validate input\nStep 2: Process request"
note right of DB: "This is a\nmulti-line\nnote"

# Conditions - quotes required for multiline
if "user is authenticated\nand has permission"
  UI -> DB: "Fetch user data"
end

# Dividers - quotes required for multiline labels
divider delay: "Wait for user\ninput here"
```

## ⚙️ **SPECIAL FEATURES**

### Comments:
```
# Full line comment
Agent -> Agent  # End of line comment
```

### Multiline Support:
```
title "Multi\nLine\nTitle"
if "condition that\nspans multiple\nlines"
  Agent -> Agent: "message\nwith\nnewlines"
end
```

### Agent Ordering:
```
define Baz, Foo, Bar      # Specify display order
```

### Short-Lived Agents:
```
A -> *B: create B         # Create B during message
B -> C                    # B exists
C -> !B: destroy B        # Destroy B during message
```

## ❌ **COMMON ERRORS TO AVOID**
```
"repeat" until x          # ERROR: Keywords cannot be quoted
A -> +                    # ERROR: Missing agent name
A -> ++B                  # ERROR: Duplicate flags
Foo is                    # ERROR: Empty agent options
note between A: hi        # ERROR: Need 2+ agents for "between"
state over A, B: hi       # ERROR: State supports only 1 agent
terminators xyz           # ERROR: Invalid terminator type (use: none, box, bar, cross, fade)
headers abc               # ERROR: Invalid header type (use: none, box, bar, cross, fade)
terminators               # ERROR: Missing terminator value
headers                   # ERROR: Missing header value
divider with height -5    # ERROR: Negative height
divider with height abc   # ERROR: Non-numeric height

# ⚠️ CRITICAL: Escape sequence errors (very common!)
A -> B: word\nbreak       # ERROR: Renders literally, use "word\nbreak" instead
note over A: line1\nline2 # ERROR: Renders literally, use "line1\nline2" instead
title Multi\nLine         # ERROR: Renders literally, use "Multi\nLine" instead
```

## 🔧 **DEFAULT VALUES**
- `headers`: `box`
- `terminators`: `none`
- Divider height (line/space/tear): `6`
- Divider height (delay): `30`
- Auto-label counter start: `1`, increment: `1`

---

## 📚 **COMPLETE SYNTAX SPECIFICATION**

### Parser Source Files:
- **Main Parser:** `scripts/sequence/parser/Parser.mjs` - Contains all grammar rules and keywords
- **Tokenizer:** `scripts/sequence/parser/Tokeniser.mjs` - Defines lexical tokens and special characters
- **Markdown Parser:** `scripts/sequence/parser/MarkdownParser.mjs` - Text formatting support
- **Pattern Parser:** `scripts/sequence/parser/LabelPatternParser.mjs` - Auto-labeling pattern parsing

### Comprehensive Test Coverage:
- **Parser Tests:** `scripts/sequence/parser/Parser_spec.mjs` - 980+ lines covering all syntax features
- **Tokenizer Tests:** `scripts/sequence/parser/Tokeniser_spec.mjs` - 380+ lines of lexical analysis tests
- **Markdown Tests:** `scripts/sequence/parser/MarkdownParser_spec.mjs` - Text formatting tests

### Valid Terminator & Header Types:
```
# Both terminators and headers accept the same 5 values:
none      # No visual terminator/header
box       # Rectangular box shape
bar       # Horizontal bar
cross     # X-shaped mark
fade      # Gradient fade effect
```

**Defaults & Usage:**
- `terminators` default: `none` - Applied to agent lifeline endings
- `headers` default: `box` - Applied to first agent begin statement
- Both commands use identical value sets but affect different diagram parts

### Arrow Construction Matrix:
All arrows are constructed from these components:
```
Line types (middle):    -    --    ~         (solid, dashed, wave)
Left terminators:       ∅    <     <<    ~    (none, arrow, double, fade)
Right terminators:      ∅    >     >>    ~    x    (none, arrow, double, fade, lost)
```

### Agent Flag Combinations:
```
Valid single flags:     +Agent    -Agent    *Agent    !Agent
Valid combinations:     +*Agent   *+Agent   -!Agent   !-Agent
Invalid (error):        ++Agent   --Agent   **Agent   !!Agent
```

### Note Position Options:
```
Directional (with/without "of"):
- note left of Agent / note left Agent
- note right of Agent / note right Agent

Spanning:
- note over Agent (single agent)
- note over Agent1, Agent2, ... (multiple agents)
- note between Agent1, Agent2, ... (2+ agents required)
```

### Divider Type Details:
```
Type        Default Height    Description
line        6                Horizontal line
space       6                Empty space
delay       30               Delay indicator with slanted lines
tear        6                Torn paper effect
```

### Auto-Label Counter Formats:
```
<inc>       → 1, 2, 3, 4, ...
<inc 5>     → 5, 6, 7, 8, ...
<inc 1,2>   → 1, 3, 5, 7, ...
<inc 01>    → 01, 02, 03, 04, ...
<inc 1.0>   → 1.0, 2.0, 3.0, 4.0, ...
```

### Delayed Connection Syntax:
```
# Start delayed connection (no label allowed)
Agent1 -> ...connection_id

# Complete delayed connection (label allowed)
...connection_id -> Agent2: Optional label

# Multiple delayed connections can interleave
A -> ...id1
B -> ...id2
...id1 -> C: First message
...id2 -> D: Second message
```

### Parallel Execution Markers:
```
# Define a marker point
marker_name:
  Agent1 -> Agent2

# Return to marker for parallel execution
simultaneously with marker_name:
  Agent3 -> Agent4

# Return to top of sequence
simultaneously:
  Agent5 -> Agent6
```

---

**Generated from:** Complete analysis of the SVG Sequence Diagram codebase including all parser files, test suites, and grammar specifications. This reference covers 100% of the documented DSL syntax as implemented in the source code.