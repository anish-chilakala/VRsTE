# VRSTE CAD Analyzer - Standalone Version

**100% Free - No API Required!**

Rule-based geometric analysis backend for CAD models. Uses mathematical algorithms and engineering heuristics instead of AI.

## Key Benefits

✅ **Completely Free** - No API costs, no subscriptions  
✅ **No External Dependencies** - Runs entirely locally  
✅ **Fast Analysis** - Instant results without API calls  
✅ **Privacy** - Your CAD files never leave your server  
✅ **Reliable** - Deterministic, reproducible results  

## Currently Supported Formats

- **STL** (Binary & ASCII) - Full geometric analysis ✨ **Best Support**
- **OBJ** - Basic analysis
- STEP, IGES, SAT - Not yet supported (convert to STL first, or use AI version)

## What It Detects

### STL Analysis (Comprehensive)
- ✅ **Non-manifold geometry** - Invalid edges shared by wrong number of faces
- ✅ **Degenerate triangles** - Extremely small or zero-area faces
- ✅ **Poor triangle quality** - High aspect ratios that cause meshing issues
- ✅ **Invalid normals** - Incorrect surface orientations
- ✅ **Thin walls** - Potentially weak structural sections
- ✅ **Scale issues** - Incorrect units or extreme dimensions
- ✅ **Model statistics** - Volume, triangle count, bounding box

### OBJ Analysis (Basic)
- ✅ Vertex and face counting
- ✅ Basic geometry validation

## Quick Start

### Installation

```bash
# Install dependencies (only Flask!)
pip install -r requirements_standalone.txt

# Run the server
python vrste_backend_standalone.py
```

That's it! No API keys, no configuration needed.

### Server Info
- Default URL: `http://localhost:5000`
- Health check: `GET /health`
- Analysis: `POST /api/analyze`

## API Usage

### Analyze STL File

```javascript
// Frontend integration example
async function analyzeSTL(file) {
  const formData = new FormData();
  formData.append('file', file);
  
  const response = await fetch('http://localhost:5000/api/analyze', {
    method: 'POST',
    body: formData
  });
  
  const result = await response.json();
  console.log(`Found ${result.summary.total_issues} issues`);
  console.log(`Health Score: ${result.model_health_score}/100`);
  
  return result;
}
```

### Example Response

```json
{
  "status": "success",
  "file_name": "robot_arm.stl",
  "model_stats": {
    "triangle_count": 5234,
    "vertex_count": 15702,
    "volume": 1234.56,
    "bounding_box": {
      "min": [0, 0, 0],
      "max": [100, 50, 75],
      "size": [100, 50, 75]
    }
  },
  "summary": {
    "total_issues": 3,
    "critical": 1,
    "high": 1,
    "medium": 1,
    "low": 0
  },
  "issues": [
    {
      "id": "ISS-001",
      "severity": "critical",
      "category": "geometric",
      "title": "Non-manifold geometry detected",
      "description": "Found 23 non-manifold edges...",
      "solution": {
        "steps": [
          "Import model into CAD software",
          "Use 'Repair' or 'Make Manifold' tool",
          "..."
        ],
        "estimated_time": "15-45 minutes",
        "difficulty": "medium"
      }
    }
  ],
  "model_health_score": 75,
  "estimated_fix_time": "1.5 hours"
}
```

## How It Works

### STL Analysis Pipeline

1. **File Parsing** - Detects and parses binary or ASCII STL format
2. **Topology Analysis** - Checks edge connectivity for manifold errors
3. **Quality Metrics** - Evaluates triangle shape, size, and distribution
4. **Geometric Validation** - Verifies normals, detects degenerates
5. **Structural Analysis** - Identifies thin walls and weak points
6. **Issue Classification** - Assigns severity and priority to each problem
7. **Solution Generation** - Provides step-by-step fix instructions

### Algorithms Used

- **Manifold Detection**: Edge-face connectivity graph analysis
- **Triangle Quality**: Aspect ratio and edge length calculations
- **Thin Wall Detection**: Proximity analysis of parallel surfaces
- **Volume Calculation**: Divergence theorem on triangulated surface
- **Normal Validation**: Vector magnitude and consistency checks

## Comparison: Standalone vs AI Version

| Feature | Standalone | AI Version |
|---------|-----------|-----------|
| **Cost** | Free ✅ | Paid API |
| **Speed** | Instant | 2-10 seconds |
| **STL Analysis** | Comprehensive ✅ | Comprehensive ✅ |
| **STEP/IGES** | ❌ Not supported | ✅ Supported |
| **Issue Detection** | Rule-based | AI-powered |
| **Explanations** | Template-based | Natural language |
| **Setup** | 1 command | API key needed |
| **Privacy** | 100% local ✅ | Files sent to API |

## When to Use Each Version

### Use Standalone If:
- Working with STL files
- Want instant, free analysis
- Need 100% privacy/offline capability
- Don't need natural language explanations
- Want deterministic, reproducible results

### Use AI Version If:
- Need STEP, IGES, or other CAD formats
- Want sophisticated contextual analysis
- Need natural language explanations
- Budget allows API costs
- Want state-of-the-art AI insights

## Converting Other Formats to STL

Most CAD software can export to STL:

**SolidWorks**: File → Save As → STL  
**Fusion 360**: File → Export → STL  
**Blender**: File → Export → STL  
**FreeCAD**: File → Export → Mesh Formats → STL  
**Onshape**: Right-click part → Export → STL  

**Tip**: Use binary STL format for better performance and smaller file size.

## Configuration

Environment variables (optional):

```bash
export MAX_FILE_SIZE_MB=50
export ALLOWED_FILE_TYPES=STL,OBJ
export PORT=5000
export HOST=0.0.0.0
```

## Production Deployment

### Using Gunicorn

```bash
gunicorn -w 4 -b 0.0.0.0:5000 vrste_backend_standalone:app
```

### Using Docker

```dockerfile
FROM python:3.12-slim

WORKDIR /app
COPY requirements_standalone.txt .
RUN pip install -r requirements_standalone.txt

COPY vrste_backend_standalone.py .

EXPOSE 5000
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "vrste_backend_standalone:app"]
```

Build and run:
```bash
docker build -t vrste-standalone .
docker run -p 5000:5000 vrste-standalone
```

## Limitations

### Current Limitations
- STEP, IGES, SAT formats not yet supported (convert to STL first)
- Assembly analysis limited (analyze individual parts)
- Material properties not analyzed (geometric only)
- FEA-level stress analysis not included

### Planned Features
- PLY format support
- Advanced mesh quality metrics
- Automated repair suggestions
- Export repair scripts
- 3D visualization endpoint

## Performance

- **Small models** (<10K triangles): <100ms
- **Medium models** (10K-100K triangles): 100-500ms
- **Large models** (>100K triangles): 500ms-2s

Memory usage: ~50MB base + ~1MB per 10K triangles

## Troubleshooting

**"Could not parse STL file"**
- Verify file is valid STL format
- Check file isn't corrupted
- Try exporting again from CAD software

**"No triangles found"**
- File may be ASCII STL with incorrect format
- Try exporting as binary STL instead

**Analysis too slow**
- Reduce triangle count (simplify mesh)
- Use binary STL instead of ASCII
- Increase server resources

## Integration Examples

### Python Client

```python
import requests

def analyze_stl_file(filepath):
    with open(filepath, 'rb') as f:
        files = {'file': f}
        response = requests.post(
            'http://localhost:5000/api/analyze',
            files=files
        )
    return response.json()

result = analyze_stl_file('model.stl')
print(f"Health Score: {result['model_health_score']}/100")
```

### React Component

```jsx
function STLAnalyzer() {
  const [result, setResult] = useState(null);
  
  const handleUpload = async (e) => {
    const file = e.target.files[0];
    const formData = new FormData();
    formData.append('file', file);
    
    const res = await fetch('http://localhost:5000/api/analyze', {
      method: 'POST',
      body: formData
    });
    
    setResult(await res.json());
  };
  
  return (
    <div>
      <input type="file" accept=".stl" onChange={handleUpload} />
      {result && (
        <div>
          <h3>Health Score: {result.model_health_score}/100</h3>
          <p>Issues: {result.summary.total_issues}</p>
        </div>
      )}
    </div>
  );
}
```

## License

MIT License - Use freely in commercial and personal projects

## Support

For issues or questions:
- Check troubleshooting section
- Review API documentation
- Submit issues on GitHub

## Contributing

Contributions welcome! Especially:
- Additional file format support (STEP, IGES)
- More geometric analysis algorithms
- Performance optimizations
- Bug fixes and improvements

---

**Ready to analyze?** Run `python vrste_backend_standalone.py` and start detecting CAD issues instantly!
