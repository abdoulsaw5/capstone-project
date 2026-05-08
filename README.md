# Monitoring Component (Dashboard)

## Overview

The Monitoring component provides a real-time dashboard interface for SOC managers to monitor the Security Alert Triage Bot's performance and effectiveness. It displays key metrics including triage volume over time, severity distribution of alerts, and response time analytics in an intuitive "Command Center" view. This component enables security teams to quickly assess system health, identify trends in security threats, and make data-driven decisions about resource allocation and incident response strategies.

## Architecture Integration

### Inputs
- **Airtable Records**: Reads all processed alert records from the shared Airtable base, including fields such as `alert_id`, `severity`, `is_true_positive`, `status`, `normalized_at`, `analyzed_at`, `resolved_at`, and timestamps for tracking processing times.

### Outputs
- **Real-time Dashboard**: Displays interactive charts and metrics to SOC managers via a Streamlit web interface, providing visual insights into the triage system's performance without requiring direct database access.

### Component Connections
- **Upstream Dependencies**: Depends on the Ingestion component (for normalized alerts), AI Core component (for triage recommendations), and Specialist component (for ticket creation and resolution updates) to populate the Airtable database with processed data.
- **Downstream Consumers**: Serves as the primary user interface for security managers, consuming data from all other components but not producing data that feeds back into the triage pipeline.

## Setup Instructions

### Prerequisites
1. **Airtable Account**: Access to the shared Airtable base containing the Alerts table with the defined schema.
2. **Streamlit Account**: For deployment (optional, can run locally).
3. **Python Environment**: Python 3.8+ with required packages.

### Required Accounts and Keys
- **Airtable API Key**: Generate a personal access token from your Airtable account settings.
- **Airtable Base ID**: The unique identifier for the shared Security Alert Triage Bot base.

### Configuration Steps

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd capstone-project/dashboard
   ```

2. **Install Dependencies**:
   ```bash
   pip install streamlit pyairtable pandas plotly
   ```

3. **Configure Secrets**:
   Create a `.streamlit/secrets.toml` file in the dashboard directory:
   ```toml
   [airtable]
   api_key = "your_airtable_personal_access_token_here"
   base_id = "your_airtable_base_id_here"
   table_name = "Alerts"
   ```

4. **Environment Variables** (Alternative to secrets.toml):
   Set the following environment variables:
   ```bash
   export AIRTABLE_API_KEY="your_airtable_personal_access_token_here"
   export AIRTABLE_BASE_ID="your_airtable_base_id_here"
   export AIRTABLE_TABLE_NAME="Alerts"
   ```

5. **Run the Dashboard**:
   ```bash
   streamlit run app.py
   ```

6. **Access the Dashboard**:
   Open your browser to `http://localhost:8501` to view the monitoring dashboard.

### Deployment (Optional)
For production deployment, use Streamlit Cloud:
1. Push your code to GitHub
2. Connect your repository to Streamlit Cloud
3. Add the Airtable secrets in the Streamlit Cloud dashboard
4. Deploy and share the public URL with your team

## Testing

### Prerequisites for Testing
- Airtable base populated with sample alert records (use the team's shared test data)
- All secrets configured correctly
- Local Streamlit server running

### Test Steps

1. **Verify Data Connection**:
   - Launch the dashboard with `streamlit run app.py`
   - Check that the dashboard loads without errors
   - Confirm that sample alert data appears in the tables and charts

2. **Test Real-time Updates**:
   - Add a new alert record to Airtable via the Ingestion component
   - Refresh the dashboard (or wait for auto-refresh if implemented)
   - Verify that the new alert appears in the metrics and charts

3. **Validate Metrics Calculations**:
   - Manually count alerts in different severity categories
   - Compare with dashboard severity distribution chart
   - Check response time calculations against raw timestamp data

4. **Test Chart Interactivity**:
   - Click on different chart elements (bars, lines, etc.)
   - Verify that filtering or drill-down functionality works as expected
   - Test time range selectors for historical data views

5. **Performance Testing**:
   - Load the dashboard with 100+ sample records
   - Monitor page load times and chart rendering performance
   - Test with multiple concurrent users if deployed

### Expected Results
- Dashboard displays without errors
- All charts populate with data from Airtable
- Metrics update in real-time as new alerts are processed
- Charts are interactive and provide meaningful insights

## Known Limitations

- **Airtable Schema Dependency**: The dashboard assumes the final Airtable schema as documented. Any changes to field names or types may require code updates.
- **API Rate Limits**: Subject to Airtable's API rate limits (5 requests per second for free plans), which may cause delays with high-volume alert processing.
- **Real-time Updates**: Currently relies on page refreshes or manual polling. True real-time streaming would require additional infrastructure.
- **Data Volume**: Performance may degrade with very large datasets (>10,000 records) without pagination or data aggregation optimizations.
- **Authentication**: No built-in user authentication or role-based access control in the current implementation.
- **Offline Capability**: Requires internet connectivity to access Airtable data and cannot function offline.
- **Mobile Responsiveness**: Dashboard optimized for desktop viewing; mobile experience may be limited.
- **Historical Data Retention**: Depends on Airtable's data retention policies and storage limits.
