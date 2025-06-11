# MCP Server Primitives: Resources, Tools, and Prompts

## Introduction

MCP servers let you build tools for everything. They are one of the three most important innovations for evolving your engineering from AI coding to agentic coding. With new models like Claude 4 and the brand new Deepseek R1.1, we have more intelligence to build than ever before. However, the models are no longer the limiting factor for your engineering output.

**Key Question:** What's limiting us as engineers from creating more value faster than ever?

**Answer:** Our ability to create capabilities for our agentic coding tools like Claude Code.

## The MCP Server Primitive Hierarchy

### The Tier List (in reverse order of capability)
1. **Resources** - Most engineers skip these
2. **Tools** - Most engineers go all-in on these
3. **Prompts** - The highest leverage primitive (most engineers miss this completely)

> Tool calling is just the beginning of your MCP server. Let me show you how to maximize its value.

## Working with the Quick Data MCP Server

### Initial Setup
- Six MCP servers available in the demo
- Using Quick Data MCP server for arbitrary data analysis on JSON and CSV files
- Running with Sonnet 4 fast workhorse model

### The Problem with Tools-Only Approach
Right away, we encounter a problem: **No idea what the MCP server can do without external documentation**.

## Understanding Tools

### Basic Tool Examples

#### 1. Load Dataset
```
Tool: load_dataset
Parameters: 
- file_path: path to JSON/CSV file
- dataset_name: e-commerce orders
```

#### 2. Dataset Breakdown
```
Tool: get_dataset_breakdown
Parameters:
- dataset_name: e-commerce orders
Returns: shape and key information about dataset
```

#### 3. Suggest Analysis
```
Tool: suggest_analysis
Parameters:
- dataset_name: ecom...
Returns: Analysis suggestions based on dataset
```

#### 4. Execute Arbitrary Code
```
Tool: execute_code
Capability: Run custom analysis code
Example: Find top three region order values
```

### Key Insights from Tool Usage
- Electronics produce significant value in e-commerce orders
- Regional analysis shows: East Coast > West Coast > Midwest
- Tools can create visualizations (pie charts, etc.)

## The Power of MCP Server Prompts

### Why Prompts Are Superior

Prompts provide three massive advantages over tools:

1. **Quick Reference**: With Claude Code, reference all prompts in a clean, detailed way
2. **Tool Composition**: Prompts can compose multiple tools together
3. **Guided Experience**: Prompts provide next steps and guidance

### Prompt Examples

#### 1. List MCP Assets Prompt
```
/quick-data
```
- Shows all available capabilities
- Loads everything fresh in context window
- Provides quick start flow

#### 2. Find Data Sources Prompt
```
/find [directory_path]
```
- Discovers available data files
- Presents them as load options
- Suggests next steps

#### 3. Dataset First Look Prompt
```
/first_look [dataset_name]
```
- Kicks off one or more tools
- Provides breakdown of dataset
- Includes sample data

#### 4. Correlation Investigation Prompt
```
/correlation_investigation [dataset_name]
```
- Finds correlations in dataset
- Can trigger multiple tool calls
- Provides analysis insights

## Codebase Architecture

### Directory Structure
```
architecture/modular/
├── data/
├── src/mcp_server/
│   ├── tools/
│   ├── resources/
│   └── prompts/
└── trees/  # for multi-agent parallel AI coding
```

### Best Practices
- Single-function Python files for isolation and testing
- Clear separation of primitives
- Modular architecture

## Key Concepts

### Tools vs Prompts
- **Tools**: Individual actions (e.g., load dataset)
- **Prompts**: Recipes for repeat solutions (AI Developer Workflows)

### The Big Three of AI Coding
1. **Context**
2. **Model** 
3. **Prompt**

These principles never go away and are always present in AI coding.

## Practical Benefits

### Speed and Focus
- No need to leave terminal/Claude Code
- Minimal information required
- Fast operation within MCP server

### Team Collaboration
- Easy handoff to engineering teams
- Public exposure of MCP servers
- Guided workflows for domain-specific problems

### Discovery and Usage
- Prompts prime agent's memory
- Quick setup with essential information
- Next steps always available

## Key Takeaways

1. **MCP servers are more than just tools** - Tool calling is just the beginning
2. **Prompts are end-to-end developer workflows** - True AI Developer Workflows (ADWs)
3. **Think domain-specific** - Build MCP servers to solve specific problems with automated, repeat solutions
4. **Guide the experience** - Use prompts to provide direction and next steps

## Summary

With prompts, you can build high-quality MCP servers that do more than just call tools. Tools are the primitives of MCP servers, not the end state. Prompts represent end-to-end developer workflows that are truly agentic workflows, doing developer work powered by Gen AI.

---

*Note: This codebase example demonstrates concrete implementation of prompts inside MCP servers. Boot up Claude Code with the provided `.mcp.json` file to explore.*