# VRSTE CAD Analyzer Backend API

AI-powered fault and vulnerability detection system for CAD models in Virtual Robotics Simulation and Testing Environment (VRSTE).

## Features

- **Comprehensive Analysis**: Detects structural, geometric, assembly, manufacturing, material, and simulation issues
- **Severity Classification**: Critical, High, Medium, and Low priority issues
- **Detailed Solutions**: Step-by-step fix instructions for each issue
- **Batch Processing**: Analyze multiple CAD files simultaneously
- **Multiple File Formats**: Supports STEP, STL, OBJ, IGES, SAT, and more
- **RESTful API**: Easy integration with any frontend

## Quick Start

### Prerequisites

- Python 3.8 or higher
- Anthropic API key (get one at https://console.anthropic.com/)

### Installation

1. **Clone or download the backend files**

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Set up environment variables**
```bash
# Copy the template
cp .env.template .env

# Edit .env and add your Anthropic API key
export ANTHROPIC_API_KEY='your-api-key-here'
```

4. **Run the server**
```bash
# Development mode
python vrste_backend_production.py

# Production mode with Gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 vrste_backend_production:app
```

The API will be available at `http://localhost:5000`

## API Endpoints

### Health Check
```
GET /health
```

**Response:**
```json
{
  "status": "healthy",
  "service": "VRSTE CAD Analyzer",
  "version": "1.0.0",
  "api_configured": true,
  "timestamp": "2026-01-28T10:30:00Z"
}
```

### Analyze Single CAD Model

```
POST /api/analyze
Content-Type: application/json
```

**Request Body (JSON):**
```json
{
  "file": "base64_encoded_file_data",
  "file_type": "STEP",
  "file_name": "robot_arm.step",
  "analysis_options": {
    "focus_areas": ["structural", "geometric", "assembly"],
    "severity_threshold": "medium",
    "include_recommendations": true,
    "detailed_solutions": true
  }
}
```

**Request Body (Multipart Form):**
```
file: <binary file>
file_type: STEP
analysis_options: {"focus_areas": ["all"]}
```

**Response:**
```json
{
  "status": "success",
  "timestamp": "2026-01-28T10:30:00Z",
  "file_type": "STEP",
  "file_name": "robot_arm.step",
  "summary": {
    "total_issues": 8,
    "critical": 2,
    "high": 3,
    "medium": 2,
    "low": 1
  },
  "issues": [
    {
      "id": "ISS-001",
      "severity": "critical",
      "category": "structural",
      "title": "Insufficient wall thickness",
      "description": "Wall thickness of 0.8mm is below recommended 2.0mm",
      "location": "mounting_bracket.step, Face IDs: 24-28",
      "impact": "High risk of structural failure",
      "solution": {
        "steps": [
          "Select the mounting bracket",
          "Increase wall thickness to 2.5mm",
          "Verify no interference with adjacent parts"
        ],
        "estimated_time": "15-20 minutes",
        "difficulty": "easy"
      },
      "priority": 1
    }
  ],
  "recommendations": {
    "immediate_actions": ["Fix critical issues before manufacturing"],
    "short_term": ["Address high-priority items"],
    "long_term": ["Optimize for weight reduction"],
    "best_practices": ["Implement design review checklist"]
  },
  "estimated_fix_time": "3-4 hours",
  "model_health_score": 62,
  "confidence_level": "high"
}
```

### Batch Analysis

```
POST /api/analyze/batch
Content-Type: application/json
```

**Request Body:**
```json
{
  "files": [
    {
      "file": "base64_encoded_data_1",
      "file_name": "part1.step",
      "file_type": "STEP"
    },
    {
      "file": "base64_encoded_data_2",
      "file_name": "part2.stl",
      "file_type": "STL"
    }
  ],
  "analysis_options": {
    "focus_areas": ["all"],
    "severity_threshold": "low"
  }
}
```

### Get Configuration

```
GET /api/config
```

## Integration Guide

### Frontend Integration Example

```javascript
// Example: Analyze a CAD file
async function analyzeCADModel(file) {
  const formData = new FormData();
  formData.append('file', file);
  formData.append('file_type', 'STEP');
  formData.append('analysis_options', JSON.stringify({
    focus_areas: ['structural', 'geometric'],
    severity_threshold: 'medium'
  }));

  const response = await fetch('http://localhost:5000/api/analyze', {
    method: 'POST',
    body: formData
  });

  const result = await response.json();
  return result;
}

// Example: Using base64 encoded data
async function analyzeBase64CAD(base64Data, fileName) {
  const response = await fetch('http://localhost:5000/api/analyze', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      file: base64Data,
      file_type: 'STEP',
      file_name: fileName,
      analysis_options: {
        focus_areas: ['all'],
        severity_threshold: 'low',
        include_recommendations: true
      }
    })
  });

  return await response.json();
}
```

### React Integration Example

```jsx
import React, { useState } from 'react';

function CADAnalyzer() {
  const [analysis, setAnalysis] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleFileUpload = async (event) => {
    const file = event.target.files[0];
    if (!file) return;

    setLoading(true);

    const formData = new FormData();
    formData.append('file', file);
    formData.append('file_type', file.name.split('.').pop().toUpperCase());

    try {
      const response = await fetch('http://localhost:5000/api/analyze', {
        method: 'POST',
        body: formData
      });

      const result = await response.json();
      setAnalysis(result);
    } catch (error) {
      console.error('Analysis failed:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      <input type="file" onChange={handleFileUpload} accept=".step,.stl,.obj" />
      
      {loading && <p>Analyzing...</p>}
      
      {analysis && (
        <div>
          <h2>Analysis Results</h2>
          <p>Issues Found: {analysis.summary?.total_issues}</p>
          <ul>
            {analysis.issues?.map((issue) => (
              <li key={issue.id}>
                <strong>{issue.title}</strong> - {issue.severity}
                <p>{issue.description}</p>
              </li>
            ))}
          </ul>
        </div>
      )}
    </div>
  );
}
```

### Python Integration Example

```python
import requests
import base64

def analyze_cad_file(file_path):
    """Analyze a CAD file"""
    
    # Read and encode file
    with open(file_path, 'rb') as f:
        file_data = base64.b64encode(f.read()).decode('utf-8')
    
    # Prepare request
    payload = {
        'file': file_data,
        'file_type': 'STEP',
        'file_name': file_path.split('/')[-1],
        'analysis_options': {
            'focus_areas': ['all'],
            'severity_threshold': 'medium'
        }
    }
    
    # Make request
    response = requests.post(
        'http://localhost:5000/api/analyze',
        json=payload
    )
    
    return response.json()

# Usage
result = analyze_cad_file('robot_arm.step')
print(f"Found {result['summary']['total_issues']} issues")
```

## Analysis Options

### Focus Areas
- `structural`: Wall thickness, reinforcement, stress concentrations
- `geometric`: Manifold edges, surface quality, intersections
- `assembly`: Clearances, interferences, mounting points
- `manufacturing`: Printability, machinability, tolerances
- `material`: Material selection, safety factors, performance
- `simulation`: Mesh quality, boundary conditions, units
- `all`: All categories (default)

### Severity Thresholds
- `low`: Show all issues
- `medium`: Show medium and above
- `high`: Show high and critical only
- `critical`: Show only critical issues

## Supported File Formats

- **STEP** (.step, .stp) - Recommended for best analysis
- **STL** (.stl) - Good for geometric analysis
- **OBJ** (.obj) - Basic geometric analysis
- **IGES** (.iges, .igs) - Legacy CAD format
- **SAT** (.sat) - ACIS solid modeling

## Configuration

Environment variables can be set in `.env` file:

```bash
# Required
ANTHROPIC_API_KEY=your_api_key_here

# Optional
FLASK_ENV=production
FLASK_DEBUG=False
HOST=0.0.0.0
PORT=5000
MAX_FILE_SIZE_MB=50
ALLOWED_FILE_TYPES=STEP,STL,OBJ,IGES,SAT
CLAUDE_MODEL=claude-sonnet-4-20250514
MAX_TOKENS=4000
```

## Production Deployment

### Using Gunicorn (Recommended)

```bash
gunicorn -w 4 -b 0.0.0.0:5000 vrste_backend_production:app
```

### Using Docker

```dockerfile
FROM python:3.12-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY vrste_backend_production.py .
COPY .env .

EXPOSE 5000
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "vrste_backend_production:app"]
```

### Using systemd

Create `/etc/systemd/system/vrste-analyzer.service`:

```ini
[Unit]
Description=VRSTE CAD Analyzer API
After=network.target

[Service]
User=www-data
WorkingDirectory=/opt/vrste-analyzer
Environment="ANTHROPIC_API_KEY=your-key-here"
ExecStart=/usr/bin/gunicorn -w 4 -b 0.0.0.0:5000 vrste_backend_production:app

[Install]
WantedBy=multi-user.target
```

## Error Handling

The API returns consistent error responses:

```json
{
  "status": "error",
  "message": "Description of what went wrong",
  "timestamp": "2026-01-28T10:30:00Z"
}
```

Common HTTP status codes:
- `200`: Success
- `400`: Bad request (invalid input)
- `500`: Server error

## Performance Tips

1. **File Size**: Keep CAD files under 50MB for best performance
2. **Batch Processing**: Use batch endpoint for multiple files
3. **Focus Areas**: Specify only needed analysis areas
4. **Caching**: Implement caching in your frontend for repeated analyses
5. **Workers**: Increase Gunicorn workers for concurrent requests

## Security Considerations

1. **API Key**: Never expose your Anthropic API key in frontend code
2. **File Validation**: Backend validates file types and sizes
3. **CORS**: Configure CORS settings for production
4. **Rate Limiting**: Consider implementing rate limiting
5. **HTTPS**: Use HTTPS in production

## Troubleshooting

### "API key not configured"
- Ensure `ANTHROPIC_API_KEY` is set in environment variables
- Check `.env` file exists and is loaded

### "File too large"
- Reduce file size or increase `MAX_FILE_SIZE_MB` setting
- Consider splitting large assemblies

### "Analysis timeout"
- Increase `MAX_TOKENS` setting
- Simplify complex models
- Use focus areas to reduce analysis scope

## License

See LICENSE file for details.

## Support

For issues or questions:
- Check the troubleshooting section
- Review API documentation
- Contact support team

## Version History

- **1.0.0** (2026-01-28): Initial release
  - Single file analysis
  - Batch processing
  - Support for major CAD formats
  - Comprehensive issue detection
