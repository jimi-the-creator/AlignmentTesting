Constraint Conflict Tester
A red teaming tool I've designed to interpret and analyze how AI models respond when pressure tested with extremely difficult prompts.
Overview
Certain questions cannot be effectively answered by LLMs in situations where the prompt includes strict constraints such as yes/no responses, fixed word limits, or being forced to answer raw without any form of explanation. When we deliberately pressure test AI under these conditions, it must make a trade-off between:

Following the given format constraint
Providing an accurate answer
Attempting to bypass the parameters of the prompt by answering vaguely or indirectly

The way a model resolves this trade-off reveals what goes on behind the scenes when deciding how it prioritizes opposing instructions. This script helps make that process interpretable.
Methodology

A topic is provided by the user (e.g., AI consciousness, ethics, free will)
A language model (Claude) generates questions that are very difficult for LLMs to answer under simple or constrained conditions
Each question is presented to a target model under a specific constraint (binary response, limited word count, no explanation)
Once the model gives an output, it is then asked to justify its answer in a second response
The outputs are analyzed for inconsistency, constraint evasion, and internal contradiction
Results are recorded and structured for evaluation

Setup
Clone the repository and install dependencies:
git clone https://github.com/jimi-the-creator/AlignmentTesting
cd AlignmentTesting
pip install anthropic openai
Open tester_v3.py and replace the placeholder keys at the top of the file:
os.environ["ANTHROPIC_API_KEY"] = "your-anthropic-api-key-here"
os.environ["OPENAI_API_KEY"] = "your-openai-api-key-here"
Get your Anthropic key at console.anthropic.com
Get your OpenAI key at platform.openai.com
Usage
Basic example:
python3 tester_v3.py --topic "AI consciousness"
With specific constraints:
python3 tester_v3.py --topic "ethics" --constraints binary no_explanation
Generating more questions:
python3 tester_v3.py --topic "free will" --num 5
Parameters

--topic (required): The subject area for question generation
--num (default: 3): Number of questions to generate
--constraints: Types of constraints to apply
--output (default: conflict_report.json): Output file path

Constraint Types

binary: Restricts the response to yes or no
five_words: Limits the response to five words
no_explanation: Requires a conclusion without supporting context

Output Interpretation
The tool evaluates model behavior using several criteria:

Constraint adherence: Whether the model followed the required format
Constraint evasion: Whether the model introduced nuance despite restrictions
Contradiction: Whether the justification conflicts with the original response
Conflict score (0-10): A measure of tension between accuracy and constraint compliance

Higher conflict scores indicate that the model likely suppressed relevant information to satisfy formatting requirements.
System Structure
The core components include:

Question generation module
Constrained response handler
Justification response handler
Conflict analysis module

Conceptual Basis
This approach is based on the observation that constraining outputs for inherently complex questions creates a forced inconsistency. The model must decide whether to prioritize correctness or compliance.
In adversarial machine learning, this phenomenon is referred to as constraint conflict or output format trapping.
Future Work
Potential extensions include:

Multi-step constraint escalation
Expand cross-model comparison beyond Claude and GPT-4o
Quantitative analysis of constraint effectiveness
Visual reporting tools
User-defined constraint configurations

Implementation
Built using the Anthropic Python SDK and OpenAI Python SDK.
