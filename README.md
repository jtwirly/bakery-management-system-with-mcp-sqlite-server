# Bakery Management System with MCP SQLite Server

A comprehensive bakery management system built using Model Context Protocol (MCP) and SQLite, running in Docker. This system helps bakery owners track inventory, analyze profitability, and optimize production.

## System Requirements

- Docker Desktop
- Claude Desktop
- MCP SQLite Server

## Setup Instructions

1. Clone the MCP servers repository:
```bash
git clone https://github.com/modelcontextprotocol/servers.git
cd servers/src/sqlite
```

2. Build the Docker image:
```bash
docker build -t mcp/sqlite .
```

3. Configure Claude Desktop:
Add the following to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "sqlite": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "-v",
        "mcp-test:/mcp",
        "mcp/sqlite",
        "--db-path",
        "/mcp/test.db"
      ]
    }
  }
}
```

4. Restart Claude Desktop to apply the changes

## Database Schema

### Tables

1. `suppliers`
   - id (PRIMARY KEY)
   - name
   - contact

2. `ingredients`
   - id (PRIMARY KEY)
   - name
   - unit
   - quantity
   - cost
   - supplier (FOREIGN KEY)
   - min_order_quantity

3. `products`
   - id (PRIMARY KEY)
   - name
   - price
   - category
   - available

4. `recipes`
   - product_id (FOREIGN KEY)
   - ingredient_id (FOREIGN KEY)
   - quantity

5. `inventory_logs`
   - id (PRIMARY KEY)
   - date
   - ingredient_id (FOREIGN KEY)
   - quantity
   - type

## Key Features

1. Inventory Management
   - Low stock alerts
   - Minimum order quantity tracking
   - Inventory movement logging

2. Product Management
   - Recipe management
   - Cost analysis
   - Profit margin calculation

3. Production Planning
   - Maximum production capacity calculation
   - Resource optimization
   - Production metrics

## Business Intelligence

The system provides several key analytics:

1. Low Stock Alerts
   - Monitors ingredients approaching minimum levels
   - Supplier contact information for quick reordering

2. Profitability Analysis
   - Product-wise profit margins
   - Cost breakdown by ingredient
   - Revenue projections

3. Production Metrics
   - Current production capacity
   - Resource utilization
   - Inventory turnover

## Sample Insights

- Most profitable product: Sourdough Bread (78.4% margin)
- Highest production capacity: Cinnamon Rolls (150 units)
- Critical inventory: Vanilla Extract (approaching minimum level)
- Limited production: Cheesecake (10 units due to cream cheese constraints)

## Maintenance

Regular maintenance tasks:
1. Monitor Docker container health
2. Backup SQLite database regularly
3. Update ingredient costs and supplier information
4. Review and adjust minimum order quantities based on demand

## Support

For issues with:
- MCP configuration: Check the [MCP Documentation](https://modelcontextprotocol.ai)
- Docker: Visit [Docker Documentation](https://docs.docker.com)
- SQLite: Refer to [SQLite Documentation](https://sqlite.org/docs.html)
