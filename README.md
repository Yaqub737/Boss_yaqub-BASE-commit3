# Boss_yaqub-BASE-commit3
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import {AggregatorV3Interface} from "@chainlink/contracts/src/v0.8/shared/interfaces/AggregatorV3Interface.sol";

library PriceConverter {
    
    function GetPrice() internal view returns (int256) {
        AggregatorV3Interface PriceFeeds = AggregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306);
        (,int256 Price,,,) = PriceFeeds.latestRoundData();
        return Price;
    }
    function GetConversionRate(uint256 ETHAmount) internal view returns (uint256) {
        // 10* price of 1 ETH
        uint256 ETHPriceInUSD = uint256(GetPrice());
        uint256 TotalAmountInUSD = (ETHPriceInUSD * ETHAmount) /* 1500,000000000000000000 */ / 1e18;
        return TotalAmountInUSD;

    }
}
