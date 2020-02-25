# bds-bsv 
## init.cpp
Modify SetupServerArgs method to support some new commands about kafka related startup commands.

# validation.h/validation.cpp
Add new methods

```
//get block data
UniValue myBlockToJSON(const CBlock& block, const CBlockIndex* blockindex, bool txDetails);

//get block by height
UniValue myGetBlock(const int height, const Config &config);

//get block
CBlock myGetBlockChecked(const CBlockIndex* pblockindex, const Config &config);

//send block data to kafka order by height
void myPrintBlockOrderByHeight(int& kafkaHeightRange, const Config &config);

//get blocks by height
std::vector<UniValue> myGetBlockbatch(const int heightStart, const int heightEnd, const Config &config);

//send http post
int post(const std::string& host, const std::string& port, const std::string& page, const std::string& data, std::string& response_data);
```

Modify ProcessNewBlock method to send new block to kafka by order.

# client.cpp
CRPCConvertParam vRPCConvertParams method array is added two new methods:

```
//add sendblock and sendbatchblock
{ "sendblock", 0, "height" },
{ "sendbatchblock", 0, "start_height" },
{ "sendbatchblock", 1, "end_height" },
```
# blockchain.cpp
Add new methods:

```
//rpc : send block to kafka by height
static UniValue sendblock(const Config &config, const JSONRPCRequest& request)

//rpc : send batch blocks to kafka by height
static UniValue sendbatchblock(const Config &config, const JSONRPCRequest &request)
```
