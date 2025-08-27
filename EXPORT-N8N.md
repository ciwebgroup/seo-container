# N8N Workflow Export Specifications

## Overview

This document defines the expected N8N workflow exports that will be delivered as part of the SEO Content Generation Pipeline implementation. Each workflow must be provided as a complete JSON export file ready for import into N8N instances.

## Export Requirements

### File Format Standards
- **Format**: JSON (N8N native export format)
- **Encoding**: UTF-8
- **Validation**: Must pass N8N import validation
- **Credentials**: All credential references must use placeholder names (e.g., `"credential_placeholder_name"`)
- **Environment Variables**: Use environment variable references for sensitive data

### Naming Conventions
- **Primary Workflow**: `primary_seo_content_pipeline.json`
- **Secondary Workflows**: `secondary_{workflow_name}.json`
- **Version Control**: Include version numbers in filenames for updates

## Expected Workflow Exports

### 1. Primary Workflow: SEO Content Generation Pipeline
**Filename**: `primary_seo_content_pipeline.json`

**Expected Node Structure**:
```
Trigger → Adapt_InvocationInput → Retrieve_Dependencies → Transform_WorkflowData → 
Validate_WorkflowData → Execute_ContentGeneration → Execute_SEOOptimization → 
Execute_MetadataGeneration → Execute_Publishing → Execute_PerformanceTracking → 
Log_Results → Execute_Callback
```

**Key Nodes Expected**:
- **Trigger Node**: Webhook or Schedule trigger
- **Adaptation Nodes**: Input parameter standardization
- **Retrieval Nodes**: Airtable/Outline data fetching
- **Transformation Nodes**: Data processing and validation
- **Execution Nodes**: Core content generation logic
- **Publishing Nodes**: WordPress and social media distribution
- **Monitoring Nodes**: Performance tracking and logging

### 2. Secondary Workflow: SEO Strategy Generator
**Filename**: `secondary_seo_strategy_generator.json`

**Primary Function**: Competitive analysis and content strategy formulation

**Expected Outputs**:
- Keyword analysis data
- Content architecture recommendations
- Publishing strategy parameters
- Competitor benchmark data

### 3. Secondary Workflow: Business Profile Generator
**Filename**: `secondary_business_profile_generator.json`

**Primary Function**: Company context and positioning documentation

**Expected Outputs**:
- Structured business profile data
- Service offering documentation
- Competitive positioning analysis
- Market context information

### 4. Secondary Workflow: Brand Voice Analyzer
**Filename**: `secondary_brand_voice_analyzer.json`

**Primary Function**: Brand personality and communication style definition

**Expected Outputs**:
- Brand voice guidelines
- Tone and style specifications
- Content messaging framework
- Communication preferences

### 5. Secondary Workflow: Audience Intelligence Generator
**Filename**: `secondary_audience_intelligence_generator.json`

**Primary Function**: Target audience analysis and persona development

**Expected Outputs**:
- Detailed audience personas
- Behavioral analysis data
- Content preference insights
- Engagement optimization recommendations

### 6. Secondary Workflow: Content Cluster Planner
**Filename**: `secondary_content_cluster_planner.json`

**Primary Function**: Pillar-silo-subsilo content architecture planning

**Expected Outputs**:
- Content cluster architecture
- Topic relationship mapping
- Publishing sequence optimization
- Internal linking strategy

## Technical Specifications

### Node Configuration Standards

#### HTTP Request Nodes
```json
{
  "parameters": {
    "url": "={{$node[\"WorkflowData\"].json[\"apiEndpoint\"]}}",
    "authentication": "predefinedCredentialType",
    "credential": "credential_placeholder_name",
    "method": "POST",
    "headers": {
      "Content-Type": "application/json"
    },
    "body": {
      "bodyType": "json"
    }
  }
}
```

#### Function Nodes
```json
{
  "parameters": {
    "functionCode": "// Descriptive comment about function purpose\nconst inputData = $input.all();\n\n// Processing logic here\n\nreturn outputData;"
  }
}
```

#### Set Nodes (Variable Management)
```json
{
  "parameters": {
    "values": {
      "string": [
        {
          "name": "workflow.variableName",
          "value": "={{$json[\"dataProperty\"]}}"
        }
      ]
    },
    "options": {
      "dotNotation": true
    }
  }
}
```

### Error Handling Requirements

Each workflow must include:
- **Error Trigger Nodes**: Connected to critical processing nodes
- **Retry Logic**: Exponential backoff for external API calls
- **Fallback Mechanisms**: Alternative execution paths
- **Logging Nodes**: Comprehensive error logging and notification

### Integration Specifications

#### Airtable Integration
- **Authentication**: API key via credentials
- **Operations**: GET, POST, PATCH operations
- **Error Handling**: Rate limit and connection error handling
- **Data Validation**: Schema validation for all data operations

#### WordPress Integration
- **Authentication**: REST API authentication
- **Operations**: Post creation, media upload, metadata management
- **Publishing Options**: Draft, scheduled, immediate publishing
- **SEO Integration**: Yoast SEO or RankMath compatibility

#### Google APIs Integration
- **Search Console**: Indexing requests and performance data
- **Analytics**: Goal tracking and conversion monitoring
- **PageSpeed Insights**: Performance monitoring integration
- **Authentication**: OAuth 2.0 service account credentials

## Validation Checklist

Before submitting workflow exports, ensure:

### Functional Validation
- [ ] Workflow imports successfully into N8N
- [ ] All nodes execute without errors in test environment
- [ ] Data flows correctly between all nodes
- [ ] Error handling triggers appropriately
- [ ] Output data matches expected schema

### Security Validation
- [ ] No hardcoded credentials or API keys
- [ ] All sensitive data uses environment variables
- [ ] Credential references use placeholder names
- [ ] No personal or confidential information in exports

### Performance Validation
- [ ] Workflow executes within expected time limits
- [ ] Memory usage remains within acceptable bounds
- [ ] API rate limits are respected
- [ ] Parallel processing is optimized where possible

### Documentation Validation
- [ ] All nodes have descriptive names
- [ ] Complex logic includes inline comments
- [ ] Workflow purpose and inputs are clearly documented
- [ ] Dependencies and prerequisites are specified

## Sample Export Structure

### Minimal Workflow Export Template
```json
{
  "name": "Workflow Name",
  "nodes": [
    {
      "parameters": {},
      "id": "unique-node-id",
      "name": "Descriptive Node Name",
      "type": "n8n-nodes-base.nodeType",
      "typeVersion": 1,
      "position": [x, y]
    }
  ],
  "connections": {
    "Node Name": {
      "main": [
        [
          {
            "node": "Next Node Name",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {},
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z",
  "id": "workflow-id"
}
```

## Testing Data Requirements

Along with each workflow export, provide:

### Test Input Data
- **Sample Invocation Data**: Representative input parameters
- **Mock API Responses**: Sample responses from external services
- **Test Credentials**: Non-functional credential configurations for testing

### Expected Output Data
- **Success Scenarios**: Expected outputs for successful execution
- **Error Scenarios**: Expected behavior for various error conditions
- **Performance Benchmarks**: Expected execution times and resource usage

## Deployment Instructions

### Pre-Deployment Setup
1. **Credential Configuration**: Set up all required API credentials
2. **Environment Variables**: Configure all environment-specific variables
3. **Dependency Installation**: Ensure all required N8N nodes are available
4. **Database Setup**: Initialize required database tables and relationships

### Import Process
1. **Backup Current Workflows**: Create backup of existing N8N workflows
2. **Import Workflows**: Import all workflow JSON files in dependency order
3. **Configure Credentials**: Map credential placeholders to actual credentials
4. **Test Execution**: Run test executions with sample data
5. **Activate Workflows**: Enable workflows for production use

### Post-Deployment Validation
1. **End-to-End Testing**: Execute complete workflow chains
2. **Performance Monitoring**: Monitor execution times and resource usage
3. **Error Monitoring**: Verify error handling and notification systems
4. **Data Validation**: Confirm output data quality and completeness

## Support and Maintenance

### Documentation Requirements
- **Setup Guide**: Step-by-step deployment instructions
- **Configuration Reference**: All configurable parameters and options
- **Troubleshooting Guide**: Common issues and resolution steps
- **API Reference**: External API dependencies and requirements

### Monitoring and Alerting
- **Execution Monitoring**: Real-time workflow execution tracking
- **Performance Alerts**: Notifications for performance degradation
- **Error Alerts**: Immediate notification of critical failures
- **Business Metrics**: Content performance and SEO impact tracking

### Update and Maintenance
- **Version Control**: Maintain version history of all workflow changes
- **Backup Strategy**: Regular backup of workflow configurations
- **Update Process**: Standardized process for workflow updates
- **Rollback Procedures**: Quick rollback capabilities for failed updates