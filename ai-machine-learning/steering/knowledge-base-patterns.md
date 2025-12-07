# Bedrock Knowledge Base Patterns

## Architecture Patterns

### Basic RAG Pattern
```
User Query → Retrieve from KB → Generate with Context → Response
```

### Advanced RAG Pattern
```
User Query → Query Expansion → Retrieve → Rerank → Generate → Response
```

## Document Preparation

### Chunking Strategy
- **Fixed Size**: 500-1000 tokens per chunk
- **Semantic**: Split on paragraphs/sections
- **Overlap**: 10-20% overlap between chunks
- **Metadata**: Include source, date, category

### Supported Formats
- PDF, TXT, MD, HTML, DOC, DOCX
- CSV, JSON (structured data)
- Images (with OCR)

## Query Patterns

### Simple Retrieval
```python
# Retrieve relevant documents
response = kb.retrieve(
    query="What is the refund policy?",
    max_results=5
)
```

### Filtered Retrieval
```python
# Filter by metadata
response = kb.retrieve(
    query="Product features",
    filter={
        "category": "electronics",
        "date": {"gte": "2024-01-01"}
    }
)
```

### Reranking
```python
# Improve relevance with reranking
response = kb.retrieve_and_rerank(
    query="Technical specifications",
    max_results=10,
    rerank_top_k=3
)
```

## Integration Patterns

### With Lambda
```python
def handler(event, context):
    query = event['query']
    
    # Retrieve context
    kb_response = kb.retrieve(query)
    context = "\n".join([doc['content'] for doc in kb_response])
    
    # Generate response
    prompt = f"Context: {context}\n\nQuestion: {query}"
    response = bedrock.invoke_model(prompt)
    
    return response
```

### With API Gateway
```
API Gateway → Lambda → KB Retrieval → Bedrock → Response
```

### With Step Functions
```
Start → Retrieve → Validate → Generate → Store → End
```

## Best Practices

### Do's ✅
- Index documents regularly
- Use metadata for filtering
- Implement caching for common queries
- Monitor retrieval quality
- Update embeddings when content changes
- Use appropriate chunk sizes
- Test different retrieval strategies

### Don'ts ❌
- Don't index sensitive data without encryption
- Don't skip document preprocessing
- Don't ignore retrieval metrics
- Don't use overly large chunks
- Don't forget to version your KB
- Don't mix languages in same KB
- Don't skip testing retrieval quality
