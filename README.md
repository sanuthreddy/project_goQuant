# project_goQuant
# GoQuant Order Execution and Management System (OEMS)

## Overview

**GoQuant OEMS** is a high-performance C++17 application designed for interacting with the Deribit cryptocurrency trading platform. This application supports various trading functionalities, including placing, modifying, and canceling orders, as well as managing open orders, positions, and retrieving order books. It includes a WebSocket server to subscribe clients to specific symbols and continuously stream order book updates.

## Features

- **Place Orders:** Place market and limit orders on Deribit.
- **Modify Orders:** Update existing orders with new quantities or prices.
- **Cancel Orders:** Cancel open orders by order ID.
- **Retrieve Order Book:** Fetch and display the order book for specific trading pairs.
- **View Current Positions:** Display current open positions.
- **WebSocket Server:** Allows clients to subscribe to symbols and receive real-time order book updates.
- **Supported Markets:** Spot, futures, and options for all supported symbols.

## Scope

- Supports **Spot, Futures, and Options** markets.
- Provides low-latency access to **all supported symbols** on Deribit.
- **Websocket server** that clients can connect to and subscribe to a symbol by sending a message.

## Prerequisites

- **C++ Compiler:** C++17 or later.
- **CMake:** Version 3.10 or later.
- **Visual Studio 2022:** or another compatible C++ IDE.
- **vcpkg:** A package manager for C++ libraries.

## Dependencies

- **Drogon:** For HTTP and WebSocket client/server functionality.
- **cURL:** For HTTP requests.
- **OpenSSL:** For handling secure connections.
- **JsonCpp:** For JSON parsing.

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/GoQuantOEMS.git
cd GoQuantOEMS
```

### Step 2: Install Dependencies

1. Install `vcpkg` (if not already installed):
```bash
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
.\bootstrap-vcpkg.bat
```
2. Install required packages:

```bash
.\vcpkg install drogon curl openssl jsoncpp
```

### Step 3: Set Up Environment Variables
Create a .env file in the project root directory with the following content:
```bash
API_KEY=your_api_key
SECRET_KEY=your_secret_key
```
Replace `your_api_key` and `your_secret_key` with your Deribit API credentials.

### Step 4: Configure CMake
Create a `CMakeLists.txt` file with the following content:
```bash
cmake_minimum_required(VERSION 3.10)
project(GoQuantOEMS)

set(CMAKE_CXX_STANDARD 17)

# Set VCPKG
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)
set(VCPKG_TARGET_TRIPLET "x64-windows")

# Find required packages
find_package(Drogon REQUIRED)
find_package(CURL REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(jsoncpp REQUIRED)

# Add executable
add_executable(goquant_oems main.cpp web_socket_client.cpp order_manager.cpp)

# Link libraries
target_link_libraries(goquant_oems Drogon::Drogon ${CURL_LIBRARIES} ${OPENSSL_LIBRARIES} jsoncpp)
```

### Step 5: Build the Project
Open the project folder in Visual Studio 2022.
Open `CMakeLists.txt` in Visual Studio.
Right-click on the `CMakeLists.txt` file in the Solution Explorer and choose `Build`.

### Step 6: Run the Project
Run the `goquant_oems` executable generated by the build process.

## Usage

### Example Commands

### Place an Order
```bash
const OrderParams params{"INSTRUMENT_NAME", AMOUNT, PRICE, "CLIENT_ORDER_ID", ORDER_TYPE};
order_manager.PlaceOrder(params, "buy", response);
```
### Modify an Order
```bash
order_manager.ModifyOrder("ORDER_ID", AMOUNT, PRICE, response);
```
### Cancel an Order
```bash
orderManager.cancelOrder("ORDER_ID");
```
### Get Order Book
```bash
order_manager.GetOrderBook("INSTRUMENT_NAME", response);
```
### Get Current Positions
```bash
order_manager.GetCurrentPositions("INSTRUMENT_NAME", "INSTRUMENT_TYPE", response);
```
### Get Open Orders
```bash
order_manager.GetOpenOrders(response);
```
### Open WebSocket Connection and Subscribe to Symbol
```bash
ws_client->ConnectToServer("ETH-PERPETUAL");
```
## Environment Variables
- API_KEY: Your Deribit API key.
- SECRET_KEY: Your Deribit API secret key.

## Error Handling
The application handles various errors, such as failed order placements or WebSocket reconnections. Errors are logged and printed to the console.


