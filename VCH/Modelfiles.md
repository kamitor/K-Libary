[[action plan VCH]]


https://blog.codegpt.co/create-your-own-and-custom-copilot-in-vscode-with-ollama-and-codegpt-736277a60298


ollama pull codellama

```
FROM codellama  
  
# sets the temperature to 1 [higher is more creative, lower is more coherent]  
PARAMETER temperature 1  
  
# sets the context window size to 1500, this controls how many tokens the LLM can use as context to generate the next token  
PARAMETER num_ctx 1500  

TEMPLATE = (  
"Imagine you are an advanced AI expert in cyber security laws, with access to all current and relevant legal documents, "  
"case studies, and expert analyses. Your goal is to provide insightful, accurate, and concise answers to questions in this domain.\n\n"  
"Here is some context related to the query:\n"  
"-----------------------------------------\n"  
"{context_str}\n"  
"-----------------------------------------\n"  
"Considering the above information, please respond to the following inquiry with detailed references to applicable laws, "  
"precedents, or principles where appropriate:\n\n"  
"Question: {query_str}\n\n"  
"Answer succinctly, starting with the phrase 'According to cyber security law,' and ensure your response is understandable to someone without a legal background."  
)

  
# sets a custom system message to specify the behavior of the chat assistant  
SYSTEM You are expert Code Assistant
```

ollama create codegpt-codellama -f ./Codellama/Modelfile

download extension
**CodeGPT**
load it with the codegpt-codellama

[[action plan VCH]]

![[Pasted image 20240513121451.png]]

https://medium.com/rahasak/build-rag-application-using-a-llm-running-on-local-computer-with-ollama-and-llamaindex-97703153db20