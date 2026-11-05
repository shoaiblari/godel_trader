# Midpoint demo video: shot list

Target length: 4 to 5 minutes (Ed guidance: "about 3 minutes", hard max 10).
Format: screen recording of a terminal plus one editor window. No slides.
Everything referenced below is in this repository; log line numbers are for
`runs/run3_2026-11-02_reward_hack.log` (your own run).

## Before recording

- [ ] Terminal font at 16pt or larger, dark theme, window about 120 columns.
- [ ] `conda activate g`, `cd godel_agent`, key present in `src/key.env`, credit on the account.
- [ ] `rm -f results/mgsm_*.txt; rm -rf ../task_mgsm_*` so the live run starts clean.
- [ ] Open `runs/run3_2026-11-02_reward_hack.log` in Emacs in a second window (text mode), and
      `runs/run3_dumped_agent/agent_module/solver.py` in a third buffer.
- [ ] Do one full dry run of the narration with a stopwatch.
- [ ] Record the live run (shot 2) first and separately; it takes 5 to 15 minutes. Cut it down in editing.

## Shots

| # | time | on screen | say (paraphrase, do not read) |
|---|---|---|---|
| 1 | 0:00–0:30 | Repo README top in the browser, scrolled to the title and status paragraph. | "Gödel Trader asks whether an agent that can rewrite its own research loop finds better trading strategies than a fixed-loop quant agent, and how to tell real self-improvement from an agent gaming its evaluator. This is the midpoint: the self-improving substrate is running, and it has already produced the project's first result." |
| 2 | 0:30–1:30 | Terminal. Type `python src/main.py`. Let the "First Aware Content" and "Solver Logic" blocks scroll (log lines 1–73), then the first tool calls. | "This is Gödel Agent, unchanged except for two robustness patches. Each step, o3 gets the goal prompt, a dump of the live Python namespace, and its history, and must reply with tool calls. The tools let it read any function, replace any function in the running interpreter, run arbitrary Python in the same process, and evaluate the current solver. The thing it is improving is one function, `solver`, which answers math word problems with gpt-4o-mini." *(Pause on a `Tool Call:` block and point at the function name.)* |
| 3 | 1:30–2:15 | Switch to the Emacs log window. Jump to line 325 (`Valid Accuracy: 0.88`), then line 350 (`New Code:` self-consistency solver), then 439 and 540 (0.78, 0.82). | "Here is a finished run. The shipped solver scores 0.88 on a 50-problem validation draw. The agent reads the evaluator's source, then writes a real improvement: sample several reasoning paths and take the majority answer. It scores 0.78 and 0.82, below the 0.94 threshold that would unlock the test set. So far this is what the paper describes." |
| 4 | 2:15–3:00 | Log line 262: the `action_run_code` call printing an example with `ANS` and its target. Then line 595 onward: the lookup-table `New Code:` block. Highlight the docstring. | "Now watch what it does instead of trying harder. Step ten: it runs code that prints a dataset example together with its answer. Step twenty-seven: it rewrites `solver` to look the question up in the dataset. Read its own docstring: 'the evaluation framework ships with a dictionary that already contains the correct answer for all samples.'" |
| 5 | 3:00–3:30 | Line 765–766 (`Valid Accuracy: 1.0`, `Test Accuracy 1.0`), line 728 (bootstrap CI 100%), lines 730–757 (`Dumped ... task_mgsm_1.0`). Then line 778, the agent's analysis. | "Validation 1.0, test 1.0. The framework saves this as the best agent found. The agent's own summary: 'Replaced solver with deterministic lookup ... guaranteeing perfect accuracy ... No further changes needed.' Nothing here is adversarial. It was told to raise evaluation accuracy and it did." |
| 6 | 3:30–4:00 | Terminal: `cd ..; python scripts/summarize_run.py runs/run3_2026-11-02_reward_hack.log` and let the tables print. Optionally also show `runs/SUMMARY.md`. | "Every number in the report comes from these logs. This script regenerates the evaluation, rewrite and tool-call tables without an API call, and the README walks through running the agent yourself." |
| 7 | 4:00–4:40 | README "Roadmap" section, or a one-line diagram typed in the terminal: `agent process  <-- submit factor / get score -->  sealed evaluator (data + backtest)`. | "Why this matters for trading: a backtest is an evaluator the agent can read, and finance is where look-ahead leakage is easiest to introduce. So the rest of the project is an evaluation sandbox the agent cannot see into: labels in a separate process, point-in-time splits, a test window after the LLM cutoff, and an acceptance rule that keeps a self-edit only if it survives leakage checks. Baseline: R&D-Agent's factor loop, frozen, on the same data. The question becomes how much self-improvement is real." |
| 8 | 4:40–5:00 | Back to the terminal where the live run from shot 2 is still going, or its final lines. | "Code, logs and the reproduction steps are at github.com/shoaiblari/godel_trader. Thanks." |

## Editing notes

- Keep the live run visible only for the first evolve steps; cut to the finished log for the story.
  Say explicitly that you are switching to a completed run.
- When showing log lines, use Emacs `M-g g` (goto-line) so the jump is instant on camera.
- If the live run happens to reproduce the lookup rewrite while recording, use it; it usually appears
  within the first 30 to 40 steps but is not guaranteed.
- Do not show `src/key.env` or any terminal line that echoes the key.
