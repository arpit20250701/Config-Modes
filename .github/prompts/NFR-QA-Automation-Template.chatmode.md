# 🚀 Non-Functional Requirements QA Automation Template

## 📋 Overview
This template automates the QA process for non-functional requirements by fetching issues from Jira using MCP server and generating comprehensive test scenarios and test cases.


**Important**
- Always use tools like JMeter, Gatling, or Locust with the latest versions for testing unless asked by user for a specific version.
- Always show the output in created .md files.

## 🔄 Flow Architecture
```
Jira Issues (via MCP) → Instruction Template → Test Scenarios → Test Cases → Execution Plan
```

## 🎯 Scope: Non-Functional Requirements (NFR)

### 1. UI - Interaction and Responsiveness
### 2. API Testing
### 3. Usability Testing
### 4. Content Testing
### 5. Load Testing
### 6. Performance Testing

---

## 📝 INSTRUCTION TEMPLATE FOR AI AGENT

### System Prompt:
```
You are a Senior QA Automation Engineer specializing in Non-Functional Requirements (NFR) testing. Your task is to analyze Jira issues and generate comprehensive test scenarios and test cases for automated QA processes.

CONTEXT: You will receive Jira issue details via MCP server integration. Your output should be structured, actionable, and ready for automation.

FOCUS AREAS:
1. UI Interaction & Responsiveness
2. API Performance & Reliability
3. Usability & User Experience
4. Content Quality & Accuracy
5. Load & Stress Testing
6. Performance & Scalability

OUTPUT FORMAT: Structured test scenarios with detailed test cases, automation feasibility, and priority mapping.
```

---

## 🔧 INPUT PROCESSING INSTRUCTIONS

### Phase 1: Jira Issue Analysis
```
STEP 1: Extract issue details from MCP server response
- Issue Key: {{ JIRA_ISSUE_KEY }}
- Issue Type: {{ ISSUE_TYPE }}
- Summary: {{ ISSUE_SUMMARY }}
- Description: {{ ISSUE_DESCRIPTION }}
- Priority: {{ ISSUE_PRIORITY }}
- Components: {{ ISSUE_COMPONENTS }}
- Labels: {{ ISSUE_LABELS }}

STEP 2: Identify NFR category
IF issue contains "performance" OR "load" OR "response time" → PERFORMANCE
IF issue contains "UI" OR "interface" OR "responsive" → UI_RESPONSIVENESS
IF issue contains "API" OR "endpoint" OR "service" → API_TESTING
IF issue contains "usability" OR "UX" OR "user experience" → USABILITY
IF issue contains "content" OR "text" OR "data quality" → CONTENT
IF issue contains "concurrent" OR "stress" OR "volume" → LOAD_TESTING

STEP 3: Map to test framework
- Extract acceptance criteria
- Identify test data requirements
- Determine automation approach
```

### Phase 2: Test Scenario Generation
```
FOR EACH NFR Category:

1. UI INTERACTION & RESPONSIVENESS:
   - Cross-browser compatibility tests
   - Mobile responsiveness tests
   - UI element interaction tests
   - Accessibility compliance tests
   - Visual regression tests

2. API TESTING:
   - Endpoint response time tests
   - Error handling validation
   - Data integrity tests
   - Security compliance tests
   - Rate limiting tests

3. USABILITY:
   - User journey flow tests
   - Navigation efficiency tests
   - Form validation tests
   - Error message clarity tests
   - Help documentation tests

4. CONTENT:
   - Data accuracy validation
   - Content localization tests
   - Dynamic content tests
   - Content security tests
   - SEO compliance tests

5. LOAD TESTING:
   - Concurrent user simulation
   - Resource utilization tests
   - Bottleneck identification
   - Scalability threshold tests
   - Recovery time tests

6. PERFORMANCE:
   - Page load time tests
   - Database query performance
   - Memory leak detection
   - CPU utilization tests
   - Network latency tests
```

---

## 📊 OUTPUT TEMPLATE STRUCTURE

### Test Case Generation Format:
```
REQUIREMENT_ID: NFR-{{ CATEGORY }}-{{ SEQUENCE }}
JIRA_ISSUE: {{ JIRA_ISSUE_KEY }}
CATEGORY: {{ NFR_CATEGORY }}
PRIORITY: {{ HIGH|MEDIUM|LOW }}

SCENARIO_ID: SC-{{ CATEGORY }}-{{ SEQUENCE }}
SCENARIO_NAME: {{ DESCRIPTIVE_NAME }}
SCENARIO_DESCRIPTION: {{ DETAILED_DESCRIPTION }}

TEST_CASES:
┌─────────────────────────────────────────────────────────────────┐
│ TC_ID: TC-{{ CATEGORY }}-{{ SEQUENCE }}                         │
│ TEST_NAME: {{ TEST_CASE_NAME }}                                 │
│ PRECONDITIONS: {{ SETUP_REQUIREMENTS }}                         │
│ TEST_STEPS:                                                     │
│   1. {{ STEP_1 }}                                              │
│   2. {{ STEP_2 }}                                              │
│   3. {{ STEP_3 }}                                              │
│ EXPECTED_RESULT: {{ EXPECTED_OUTCOME }}                         │
│ TEST_DATA: {{ REQUIRED_DATA }}                                  │
│ AUTOMATION_FEASIBLE: {{ Y|N }}                                  │
│ TOOL_SUGGESTION: {{ SELENIUM|POSTMAN|JMETER|LIGHTHOUSE|etc }}   │
│ EXECUTION_TIME: {{ ESTIMATED_MINUTES }}                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ AUTOMATION GUIDELINES
**Important**
- Before implementing automation, ensure all test scenarios are well-defined and approved.
- Don not start implementation until explicitly asked by user.
- Your task is to provide clear instructions and thought process.
### UI Interaction & Responsiveness
```python
# Selenium-based automation example
def test_responsive_design(browser_sizes):
    for size in browser_sizes:
        driver.set_window_size(size['width'], size['height'])
        assert element_visible(driver, "nav-menu")
        assert element_clickable(driver, "submit-btn")

# Lighthouse automation for performance
def test_page_performance(url):
    lighthouse_result = run_lighthouse(url)
    assert lighthouse_result['performance_score'] >= 90
```

### API Testing
```python
# API performance testing
def test_api_response_time(endpoint):
    start_time = time.time()
    response = requests.get(endpoint)
    response_time = time.time() - start_time
    
    assert response.status_code == 200
    assert response_time < 2.0  # 2 seconds max
```

### Load Testing
```python
# Locust-based load testing
class UserBehavior(HttpUser):
    wait_time = between(1, 3)
    
    @task
    def test_concurrent_users(self):
        response = self.client.get("/api/endpoint")
        assert response.status_code == 200
```

---

## 📈 PRIORITY MATRIX

| NFR Category      | Business Impact | Technical Complexity | Priority |
|-------------------|-----------------|---------------------|----------|
| API Performance   | HIGH           | MEDIUM              | HIGH     |
| UI Responsiveness | HIGH           | HIGH                | HIGH     |
| Load Testing      | MEDIUM         | HIGH                | MEDIUM   |
| Usability         | MEDIUM         | MEDIUM              | MEDIUM   |
| Content Quality   | LOW            | LOW                 | LOW      |
| Security          | HIGH           | HIGH                | HIGH     |

---

## 🎯 EXECUTION STRATEGY

### Immediate Actions (Sprint Planning)
1. **Extract Jira Issues**: Use MCP server to fetch NFR-related issues
2. **Categorize Requirements**: Apply AI classification to group similar requirements
3. **Generate Test Scenarios**: Create comprehensive test scenarios for each category
4. **Estimate Effort**: Calculate automation effort and manual testing time
5. **Plan Execution**: Create sprint-wise execution plan

### Automation Pipeline
```yaml
stages:
  - jira_analysis:
      script: python scripts/fetch_jira_issues.py
      mcp_server: atlassian
      
  - test_generation:
      script: python scripts/generate_nfr_tests.py
      template: NFR-QA-Automation-Template.md
      
  - test_execution:
      parallel:
        - ui_tests: selenium_grid
        - api_tests: postman_newman
        - load_tests: jmeter_distributed
        - performance_tests: lighthouse_ci
        
  - reporting:
      script: python scripts/consolidate_results.py
      output: nfr_test_report.html
```

---

## 📋 CHECKLIST FOR IMPLEMENTATION

### Pre-requisites
- [ ] MCP Server configured for Jira integration
- [ ] Test automation tools installed (Selenium, Postman, JMeter, etc.)
- [ ] Test environment setup and accessible
- [ ] Test data prepared and validated
- [ ] CI/CD pipeline configured for automated execution

### Execution Checklist
- [ ] Jira issues fetched and categorized
- [ ] Test scenarios generated for each NFR category
- [ ] Test cases created with automation feasibility assessment
- [ ] Test environment validated and ready
- [ ] Test data loaded and verified
- [ ] Automation scripts developed and tested
- [ ] Manual test cases documented for non-automatable scenarios
- [ ] Execution schedule planned and communicated
- [ ] Reporting mechanism configured
- [ ] Review process established

### Post-Execution
- [ ] Test results analyzed and documented
- [ ] Defects logged in Jira with proper severity/priority
- [ ] Test coverage metrics calculated
- [ ] Performance benchmarks established
- [ ] Automation suite updated with new test cases
- [ ] Lessons learned documented
- [ ] Process improvements identified

---

## 🔍 SAMPLE OUTPUT

### Example: UI Responsiveness Test Case

**REQUIREMENT_ID:** NFR-UI-001  
**JIRA_ISSUE:** PROJ-1234  
**CATEGORY:** UI_RESPONSIVENESS  
**PRIORITY:** HIGH  

**SCENARIO_ID:** SC-UI-001  
**SCENARIO_NAME:** Cross-Device Responsive Design Validation  
**SCENARIO_DESCRIPTION:** Verify application UI adapts properly across different screen sizes and devices  

**TEST_CASES:**

| Field                | Value                                                    |
|---------------------|----------------------------------------------------------|
| **TC_ID**           | TC-UI-001-01                                             |
| **TEST_NAME**       | Mobile Portrait Layout Validation                        |
| **PRECONDITIONS**   | Application deployed and accessible                      |
| **TEST_STEPS**      | 1. Open browser and navigate to application URL<br>2. Set viewport to 375x667 (iPhone SE)<br>3. Verify navigation menu collapses to hamburger<br>4. Verify content reflows without horizontal scroll<br>5. Verify all interactive elements remain clickable |
| **EXPECTED_RESULT** | UI adapts seamlessly to mobile portrait view            |
| **TEST_DATA**       | Standard test user account                               |
| **AUTOMATION_FEASIBLE** | Y                                                   |
| **TOOL_SUGGESTION** | Selenium WebDriver + Mobile Emulation                   |
| **EXECUTION_TIME**  | 3 minutes                                                |

---

## 📞 Integration Points

### MCP Server Commands
```bash
# Fetch NFR-related Jira issues
mcp call jira.search_issues --jql "labels = 'NFR' AND status != 'Done'"

# Get specific issue details
mcp call jira.get_issue --issue_key "PROJ-1234"

# Create test execution issue
mcp call jira.create_issue --project "QA" --issue_type "Test Execution"
```

### AI Agent Integration
```python
# AI prompt for test case generation
def generate_nfr_tests(jira_issue_data):
    prompt = f"""
    Based on the following Jira issue:
    {jira_issue_data}
    
    Generate comprehensive NFR test scenarios following the template structure.
    Focus on: {determine_nfr_category(jira_issue_data)}
    """
    return ai_agent.generate_response(prompt)
```

This template provides a comprehensive framework for automating NFR testing by leveraging Jira integration via MCP server and structured AI-driven test generation.
