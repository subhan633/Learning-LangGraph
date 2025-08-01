# Blog Generation with Sequential Workflow in LangGraph

This repository demonstrates a **sequential workflow** using [LangGraph](https://langchain-ai.github.io/langgraph/) to generate a blog post from a given title. The workflow leverages prompt chaining with an open-source LLM (via [Groq](https://groq.com)) to perform three tasks in sequence: generating an outline, writing the blog, and evaluating the blog's quality. This project showcases how LangGraph can orchestrate a multi-step process with state management, making it ideal for learning about sequential workflows and prompt chaining in LLM-based applications.

## Project Overview

The workflow consists of three nodes, executed sequentially, with a state object that tracks four key-value pairs: `title`, `outline`, `content`, and `evaluate`. Each node builds on the output of the previous one, demonstrating **prompt chaining** where the output of one LLM call is used as input for the next.

### Workflow Steps
1. **Generate Outline**: Takes a blog title and creates a structured outline (introduction, 3-5 sections, conclusion).
2. **Write Blog**: Uses the outline to generate a detailed blog post.
3. **Evaluate Blog**: Scores the blog (0-100) based on how well it adheres to the outline.

The state object (`BLOGState`) persists across nodes, ensuring data (e.g., outline, content) is passed seamlessly, showcasing LangGraph's state management capabilities.

## Repository Structure
- `3_prompt_chaining.ipynb`: Main script implementing the LangGraph workflow with three nodes.
- `.env`: Stores the Groq API key (not committed; create your own).
- Other files (e.g., additional scripts or configurations) may be included for related experiments or utilities.

## Prerequisites
- Python 3.8+
- A Groq API key (sign up at [groq.com](https://groq.com) and add it to a `.env` file as `GROQ_API_KEY=your_api_key_here`).
- Required Python packages:
  ```bash
  pip install python-dotenv langchain-groq langgraph
  ```

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/subhan633/sequential-workflow-langgraph.git
   cd your-repo-name
   ```
2. Create a `.env` file in the root directory with your Groq API key:
   ```plaintext
   GROQ_API_KEY=your_api_key_here
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   (Or manually install `python-dotenv`, `langchain-groq`, and `langgraph` as shown above.)
4. Run the main script:
   ```bash
      3_prompt_chaining.ipynb
   ```
5. The script will:
   - Take an example title ("The Benefits of Daily Meditation").
   - Generate an outline, blog content, and an integer score (0-100).
   - Print the results to the console.

## Example Output
```plaintext
Title: The Benefits of Daily Meditation
Outline:
- Introduction: Importance of meditation
- Section 1: Mental health benefits
  - Reduces stress
  - Improves focus
- Section 2: Physical health benefits
  - Lowers blood pressure
- Conclusion: Why daily meditation matters

Blog:
[Full blog content based on the outline...]

Score: 92
```

## Key Concepts Demonstrated
- **Sequential Workflow**: Nodes are executed in order (outline → blog → evaluation), with each node depending on the previous node's output.
- **Prompt Chaining**: Each node uses the LLM with a tailored prompt, passing outputs (e.g., outline to blog, blog to evaluation) to build a cohesive process.
- **State Management**: The `BLOGState` object tracks `title`, `outline`, `content`, and `evaluate` across nodes, ensuring data persistence.
- **Evaluation Logic**: The evaluation node scores the blog based on outline adherence, demonstrating how LLMs can be used for quality assessment.

## Why LangGraph?
LangGraph simplifies the creation of complex workflows by modeling tasks as a graph of nodes and edges. This project uses a linear graph for simplicity, but LangGraph supports more complex structures (e.g., conditional branching, cycles), making it a powerful tool for LLM orchestration.

## Future Improvements
- Add more evaluation criteria (e.g., clarity, engagement).
- Visualize the LangGraph workflow using graph visualization tools.
- Extend the workflow with additional nodes (e.g., editing or summarizing the blog).

## Contributing
Feel free to fork this repository, submit issues, or contribute improvements via pull requests. Suggestions for enhancing the workflow or adding new features are welcome!

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Built with [LangChain](https://www.langchain.com/), [LangGraph](https://langchain-ai.github.io/langgraph/), and [Groq](https://groq.com).
- Inspired by the need to understand sequential workflows and prompt chaining in LLM applications.