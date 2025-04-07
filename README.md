# Bakery Management System with MCP SQLite Server

A comprehensive bakery management system built using Model Context Protocol (MCP) and SQLite, running in Docker. This system helps bakery owners track inventory, analyze profitability, and optimize production. Created as part of the MIT MCP Hackathon tutorial (April 2025).

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

## About the MIT MCP Hackathon

This project was created as part of a tutorial during the MIT MCP Hackathon (April 2025), which aimed to introduce developers to the Model Context Protocol and help projects/startups launch their own MCP servers. The hackathon was part of the NANDA (Networked Agents and Decentralized AI) hub initiative at MIT.

## License

This project is a fork from https://github.com/modelcontextprotocol/servers.git

## Support

For issues with:
- MCP configuration: Check the [MCP Documentation](https://modelcontextprotocol.ai)
- Docker: Visit [Docker Documentation](https://docs.docker.com)
- SQLite: Refer to [SQLite Documentation](https://sqlite.org/docs.html)

## Screenshots
<img width="998" alt="Screen Shot 2025-04-06 at 10 35 56 PM" src="https://github.com/user-attachments/assets/0aad979c-d97b-40b3-aaf1-9d5bc3031b70" />
<img width="1009" alt="Screen Shot 2025-04-06 at 10 37 36 PM" src="https://github.com/user-attachments/assets/9e57999c-996f-4566-b7e6-915eca0f7f3b" />
<img width="1010" alt="Screen Shot 2025-04-06 at 10 40 03 PM" src="https://github.com/user-attachments/assets/bdbb5c2d-e5ff-4013-a206-67779473659f" />
<img width="969" alt="Screen Shot 2025-04-06 at 10 46 54 PM" src="https://github.com/user-attachments/assets/74abe9e8-8fa3-4663-a119-22e5f35a78c4" />
<img width="967" alt="Screen Shot 2025-04-06 at 10 47 11 PM" src="https://github.com/user-attachments/assets/98042814-58d7-4a6f-91af-a16f80f1e436" />
<img width="970" alt="Screen Shot 2025-04-06 at 10 47 22 PM" src="https://github.com/user-attachments/assets/1f14e09f-ce67-4520-ba66-87f02b27fa4d" />

## Link

https://claude.site/artifacts/2c8e5fa0-ae56-4e69-9b31-f991667c7e0c
