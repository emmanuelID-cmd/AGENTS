# API Integration

When a task requires an API or calls for an API integration, the PLANNER must
state the directory where the integration will live and provide the ordered
steps required to add it. Do not begin implementation until those directory
and integration steps are clear.

* Before requesting a paid API key, first identify and evaluate available free
  API options, free tiers, and trial access that can meet the requirement.
* When additional viable APIs exist, provide a concise recommended-options list
  that states each API’s purpose, free-tier or cost status, key limitations,
  and why it is or is not recommended.
* Request a paid API key only when the available free options cannot meet the
  documented integration requirements.
* The BUILDER must create the required `.env` file for API configuration and
  secrets as part of the integration work.
* Immediately after any `.env` file is created—whether by the user or the
  BUILDER—add that file's path to the applicable `.gitignore` file.
* Never commit API secrets, credentials, tokens, or a populated `.env` file.
* Document the required environment-variable names and where they are used,
  without recording their values.

## API State Handling

* Show the application's standard animated loading icon while an API request
  is loading.
* When an API request fails, show the Temporarily Unavailable state.
* When an API request succeeds, show the Live state with the current API
  response.

## API Internet Access

* When internet access is unavailable, show a clear No Internet Access state.
* Tell the user to try again when internet access is restored or to turn on
  internet access before retrying the API request.

---
