# FAL.AI Models Schema Data

This directory contains comprehensive schema information for all models available on fal.ai.

## Files

### `fal_models_schemas.json`

Complete schema data for 827 fal.ai models, including:
- Model metadata (id, title, category, description)
- Input parameters with types, constraints, and descriptions
- Output parameters with types and descriptions
- Documentation and playground URLs
- License information
- Tags and categorization

## Data Structure

Each model entry contains:

```json
{
  "id": "fal-ai/model-name",
  "title": "Model Display Name",
  "category": "text-to-image",
  "description": "Model description",
  "tags": ["tag1", "tag2"],
  "thumbnailUrl": "https://...",
  "playgroundUrl": "https://fal.ai/models/...",
  "documentationUrl": "https://fal.ai/models/.../api",
  "licenseType": "commercial",
  "deprecated": false,
  "unlisted": false,
  "inputParameters": {
    "param_name": {
      "type": "string|number|integer|boolean|array|object",
      "description": "Parameter description",
      "required": true|false,
      "enum": ["option1", "option2"],
      "minimum": 0,
      "maximum": 100,
      "default": "value",
      "examples": ["example1"]
    }
  },
  "outputParameters": {
    "output_name": {
      "type": "string|array|object",
      "description": "Output description"
    }
  }
}
```

## Model Categories

The dataset includes models across 22 categories:

| Category | Count |
|----------|-------|
| image-to-image | 264 |
| image-to-video | 122 |
| text-to-image | 115 |
| text-to-video | 85 |
| video-to-video | 83 |
| text-to-audio | 33 |
| vision | 29 |
| text-to-speech | 19 |
| image-to-3d | 19 |
| training | 15 |
| audio-to-audio | 11 |
| speech-to-text | 8 |
| audio-to-video | 5 |
| llm | 4 |
| 3d-to-3d | 3 |
| video-to-audio | 3 |
| json | 3 |
| speech-to-speech | 2 |
| text-to-json | 1 |
| json-to-image | 1 |
| text-to-3d | 1 |
| image-to-json | 1 |

## Usage

### Loading the data

```javascript
import modelsData from './fal_models_schemas.json';

// Find models by category
const videoModels = modelsData.filter(m => m.category === 'text-to-video');

// Find a specific model
const model = modelsData.find(m => m.id === 'fal-ai/flux-pro/kontext');

// Get all input parameters for a model
const inputParams = model.inputParameters;
```

### Example: Finding models with specific capabilities

```javascript
// Find all models that accept image input
const imageInputModels = modelsData.filter(model => 
  Object.keys(model.inputParameters).some(param => 
    param.includes('image') || 
    model.inputParameters[param].description?.toLowerCase().includes('image')
  )
);

// Find models with duration control
const durationControlModels = modelsData.filter(model =>
  'duration' in model.inputParameters
);

// Find all non-deprecated commercial models
const commercialModels = modelsData.filter(model =>
  model.licenseType === 'commercial' && !model.deprecated
);
```

## Data Generation

This data was generated using the `scripts/parse_fal_models.py` script, which:
1. Fetches all models from the fal.ai API (with pagination)
2. Retrieves OpenAPI schemas for each model
3. Parses input and output parameters with full type information
4. Extracts metadata and documentation URLs
5. Saves the structured data to JSON

To regenerate the data:

```bash
cd /path/to/videosos
python3 scripts/parse_fal_models.py
```

## Notes

- 3 models out of 830 total models did not have OpenAPI schemas available and were skipped
- All parameter constraints (min/max values, enums, etc.) are preserved
- Default values and examples are included where available
- The data includes both active and deprecated models (marked with `deprecated: true`)

## Use Cases

This data can be used to:
- Build dynamic UI for model selection and parameter configuration
- Validate user inputs against model constraints
- Generate documentation
- Implement cost estimation based on model parameters
- Create model comparison tools
- Build automated testing suites

## Last Updated

Generated on: 2025-10-30

Total models: 827
