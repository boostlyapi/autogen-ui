# autogen-ui

Run a prompt through an AutoGen AgentChat team and read its responses in a browser. autogen-ui pairs a TypeScript/Next.js chat interface with a Python/FastAPI backend, so you can try a predefined agent team without writing a separate client.

**API compatibility:** This example targets the AutoGen 0.4.x AgentChat API. Changes to that API may require updates to the app.

## Features

- Submit prompts through a browser-based chat interface.
- Run tasks with a predefined agent team configured in `notebooks/default_team.json`.
- Stream task results from the FastAPI backend to the client.
- Load a team specification through the Python manager; see `notebooks/tutorial.ipynb` for an example.

## Installation

You need Python 3.9+, Node.js, and Yarn. The frontend uses TypeScript, but the agent runner requires the Python backend too.

From the root of a local checkout of autogen-ui, install the backend and build the frontend:

```bash
pip install -e .
cd frontend
yarn install
export NEXT_PUBLIC_API_SERVER=http://localhost:8081/api
yarn build
cd ..
```

`NEXT_PUBLIC_API_SERVER` sets the backend address used by the frontend. Set it before building. Rebuild the frontend if you change that address or edit the frontend source.

## Usage

Set your OpenAI API key in the backend environment, then start the server:

```bash
export OPENAI_API_KEY=<your_key>
autogenui --port 8081
```

Open http://localhost:8081 and enter a prompt. The backend passes the prompt to the configured agent team and streams results back to the chat interface. The project name is `autogen-ui`; its Python CLI command is `autogenui`.

For development, run the backend with hot reload:

```bash
autogenui --reload
```

In another terminal, start the frontend development server:

```bash
cd frontend
export NEXT_PUBLIC_API_SERVER=http://localhost:8081/api
yarn dev
```

Use the address printed by the frontend development server. The Python CLI serves a compiled frontend; use `yarn build` to refresh that version after frontend changes.

This is a starting-point example. Authentication, authorization, database-backed interaction history, and team selection from the UI are not implemented. Keep the app local unless you add appropriate access controls.

## License

MIT. This project is based on [victordibia/autogen-ui](https://github.com/victordibia/autogen-ui). Retain the upstream copyright and MIT license notice in copies or substantial portions of the software.
