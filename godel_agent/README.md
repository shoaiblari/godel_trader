# Gödel Agent (patched copy)

This directory is a copy of the `src/` tree of
[Arvid-pku/Godel_Agent](https://github.com/Arvid-pku/Godel_Agent)
(MIT license, see `LICENSE`), at upstream commit `bbb5087` (2025-09-17),
with only the MGSM dataset kept under `datasets/`.

Local changes relative to upstream, all in `src/agent_module.py`:

1. **`truncate_repr`** – the environment summary that is sent to the planning
   LLM on every step used to print every global variable in full. When the
   agent stored the whole dataset in a global, the prompt grew past o3's
   200k-token limit and the run died (see `../runs/run1_*`). Each value is now
   cut to 300 characters plus its type and length.
2. **Full tracebacks in the log** – tool-call errors were truncated to 100
   characters when printed; they are now printed in full so failures can be
   diagnosed from the log alone.

Everything else (prompts, tool schema, evaluation thresholds, model names)
is upstream behaviour. Run it from this directory:

    cp src/key.env.example src/key.env   # then paste your OpenAI key into src/key.env
    python src/main.py
