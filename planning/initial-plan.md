# Harness design plan
## Motivation

The core goal behind this project is to be able to create, modify and work with agents and loops in a much simpler and more direct and customisable manner. Currently, the majority of loop design is done with proprietary software or requires using python libraries. The core thesis of the project is to create an easily customisable and extendable framework for building and designing agentic systems.


A system like this should be customisable enough to allow for agents to build and modify their own loops whilst maintaining the correct scope on subagents and creating safe systems.

The system being modifiable by agents directly should allow for scoping, and the standard `$ref` format provided by jsonschema should allow for easy linking between components and referencing already created systems.

## Development stages

1. Basic specification for the agentic construction finished
2. Implementation of the basic concept

## Ideas to be resolved

- We need an entry point
- We need to confirm how we are linking to resources, we need some standard definitions, maybe allow for relative path resolving and the likes???

## Ideal usage

### Example configuration

```yaml
agents:
	defaultAgent:
	  name: agent-name
	  version:
	  	versionCode: '1.0'
	  	versionStatus: stable
	  models:
	  	- $ref: "/models/deepseek-4.1-flash"
	  systemPrompt:
	  	$ref: "/prompts/standard/chatbot"

tools:
	$ref: "/tools/minimal"

loops:
	chatbot:
	  name: standard-agentic
	  events: # TODO CHANGE NAME
	  	- $ref: "/events/user-input"
	  	- $ref: "#/agents/defaultAgent"
	  repeat: true

triggers:
	startup:
		- $ref: "/actions/run"
		  target:
		  	$ref: "#/loops/chatbot"
```