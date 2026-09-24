### Yufeiyang Chen

Undergraduate in Cyber Science and Technology at Sun Yat-sen University. I have been contributing to open-source AI tooling since July 2026 and still send patches most days, mostly to evaluation and red-teaming frameworks, agent and MCP tooling, and the libraries they sit on.

Much of what I fix has the same shape. Something fails, nothing crashes, and the caller gets a value that looks like success. A failed page read comes back as if it were the page; a scanner reports that it wrote its findings when the write never happened.

#### Where I contribute

| Area | Projects |
| --- | --- |
| Evaluation and red teaming | [PyRIT](https://github.com/microsoft/PyRIT) · [inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai) · [inspect_evals](https://github.com/UKGovernmentBEIS/inspect_evals) · [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) · [opik](https://github.com/comet-ml/opik) · [uqlm](https://github.com/cvs-health/uqlm) · [trulens](https://github.com/truera/trulens) · [rhesis](https://github.com/rhesis-ai/rhesis) · [garak](https://github.com/NVIDIA/garak) · [lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval) |
| Agents, coding agents and MCP | [MCP servers](https://github.com/modelcontextprotocol/servers) · [fastmcp](https://github.com/PrefectHQ/fastmcp) · [serena](https://github.com/oraios/serena) · [letta-code](https://github.com/letta-ai/letta-code) · [pydantic-ai](https://github.com/pydantic/pydantic-ai) · [livekit agents](https://github.com/livekit/agents) · [haystack](https://github.com/deepset-ai/haystack) · [llama_index](https://github.com/run-llama/llama_index) · [griptape](https://github.com/griptape-ai/griptape) · [fantasy](https://github.com/charmbracelet/fantasy) · [mcp-context-forge](https://github.com/IBM/mcp-context-forge) · [zotero-mcp](https://github.com/54yyyu/zotero-mcp) |
| Structured generation and inference | [xgrammar](https://github.com/mlc-ai/xgrammar) · [outlines](https://github.com/dottxt-ai/outlines) · [vllm-metal](https://github.com/vllm-project/vllm-metal) |
| Tracing and observability | [openinference](https://github.com/Arize-ai/openinference) · [phoenix](https://github.com/Arize-ai/phoenix) · [openlit](https://github.com/openlit/openlit) · [langwatch](https://github.com/langwatch/langwatch) |
| Security tooling | [fickling](https://github.com/trailofbits/fickling) · [AI-Infra-Guard](https://github.com/Tencent/AI-Infra-Guard) · [agentic_security](https://github.com/msoedov/agentic_security) · [agent-sweep](https://github.com/Ishannaik/agent-sweep) |
| Data validation and ingestion | [pandera](https://github.com/unionai-oss/pandera) · [great_expectations](https://github.com/fivetran/great_expectations) · [qdrant-client](https://github.com/qdrant/qdrant-client) · [unstructured](https://github.com/Unstructured-IO/unstructured) |

#### Some pull requests I learned from

- [inspect_evals #2132](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132). With more than one epoch, Humanity's Last Exam averaged each sample across epochs before computing calibration error, so errors in opposite directions cancelled and a maximally miscalibrated run scored 0.0. Calibration is now computed per attempt, and single-epoch results are unchanged. The issue was opened by a maintainer.
- [PyRIT #2467](https://github.com/microsoft/PyRIT/pull/2467). Gave the GCG optimisation loop explicit state types. In review the maintainer caught that my first version used `inf` to mean "not measured", which would have hidden a genuine non-finite loss; it now carries an explicit flag. The issue was opened by a maintainer.
- [uqlm #459](https://github.com/cvs-health/uqlm/pull/459). When one judge in a panel ran out of retries, every aggregate for that prompt became NaN and the run still reported success. I reported it and sent the fix together.
- [lm-evaluation-harness #4039](https://github.com/EleutherAI/lm-evaluation-harness/pull/4039). MATH answer normalization turned tuple answers such as `0,1` into `01`, so correct answers were marked wrong. The maintainer kept the leaderboard copy of the function frozen, because changing it would make historical scores incomparable. I had not thought of that, and it was the right call.
- [opik #8195](https://github.com/comet-ml/opik/pull/8195). A system under evaluation could embed a verdict in its output that the judge would repeat, and the parser took the first one. My first revision escaped the values; the maintainer pointed out that rewriting the evaluated output distorts the evaluation itself, so the merged version isolates the output with namespaced delimiters instead and states the remaining risk in tests. The issue was reported by another contributor.
- [xgrammar #834](https://github.com/mlc-ai/xgrammar/pull/834). Made `prefixItems` positional, as JSON Schema Draft 2020-12 specifies. An earlier draft accepted too much; the regression matrix caught it and it was replaced.

#### failroute

[failroute](https://github.com/feiiiiii5/failroute) is a static analyzer I wrote for one family of these bugs: Python exception handlers that return something a caller cannot tell apart from success. `pip install failroute`.

Measuring it was the most useful part. On eight pinned AI packages it flags plenty that standard linters miss, but in a sample labelled by LLM agents most findings were intentional fallbacks, and among findings the linters miss, about 1 in 56 was labelled a defect. The defects it did find are also caught by `flake8 --select E722`. The repository has the full numbers and the method.

#### How I work

Before filing anything I follow the call path in the real code. When I ran failroute over PyRIT it raised several dozen warnings; I traced twelve of them, all twelve were deliberate design decisions, and I filed nothing.

I work with coding agents inside a workflow I set up myself, with my own test gates, and pull requests where AI tools shaped the change say so. Early on I gave the agents too much rope: they lost context over long runs and opened some weak and duplicate pull requests. I closed those and tightened the workflow. If one of my pull requests turns out to be wrong or not worth your time, I close it; if you find one I missed, close it or tell me. Blunt review is welcome.

Most repositories on this account are forks for upstream work.
