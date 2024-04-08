
# Zivoe contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Ethereum mainnet
___

### Q: Which ERC20 tokens do you expect will interact with the smart contracts? 
USDC, DAI, USDT, FRAX, and in some yield lockers CRV, CVX
___

### Q: Which ERC721 tokens do you expect will interact with the smart contracts? 
None
___

### Q: Do you plan to support ERC1155?
No
___

### Q: Which ERC777 tokens do you expect will interact with the smart contracts? 
None
___

### Q: Are there any FEE-ON-TRANSFER tokens interacting with the smart contracts?

No
___

### Q: Are there any REBASING tokens interacting with the smart contracts?

No
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED?
RESTRICTED
___

### Q: Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
TRUSTED
___

### Q: Are there any additional protocol roles? If yes, please explain in detail:
There are multiple roles in the protocol, the permissions of these roles are outlined (in terms of accessibility to smart contract endpoints/functions) for each contract here: https://docs.zivoe.com/developer-docs/core-contracts

See the Figma here https://www.figma.com/file/qjuQ0uGQl9QD7KeBwyf73d/Zivoe-Visualization?type=whiteboard&node-id=0-1&t=ZF3HuGmByCAkU6NT-0 for additional context on which endpoints these Roles can access

In general:
ZVL (referenced in ZivoeGlobals) will have access to protocol settings
OCC (referenced in OCC_) will have access to underwriting endpoints in that particular OCC locker
ZVE (governance) will be able to initiate proposals, vote on proposals
Pausable (multi-sig) will also have ability to "pause" proposals deemed hostile

2
Please see Figma for access to endpoints

3
Per the NatSpec

4
Only access to the provided endpoints should be allowed
___

### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
Not necessarily, other than generic ERC20 integrations from OpenZeppelin library
___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
None
___

### Q: Please provide links to previous audits (if any).
https://github.com/runtimeverification/publications/blob/main/reports/smart-contracts/Zivoe_Core_Contracts.pdf
https://github.com/runtimeverification/publications/blob/main/reports/smart-contracts/Zivoe_Locker_Contracts.pdf
___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)?
Keepers will handle conversions in the OCT_ lockers (via 1INCHv5 APIs and submitting tx's to smart contracts)
For minting tranche tokens (or participating in ITO, minting tokens there) we have front-end mechanisms to validate input
___

### Q: In case of external protocol integrations, are the risks of external contracts pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality.
Not acceptable
___

### Q: Do you expect to use any of the following tokens with non-standard behaviour with the smart contracts?
Yes, I believe it's USDT that has issues with 0 approval, we have integrated SafeERC20 to handle these situations
USDC also has 6 decimals however we've integrated adjustment/conversion helper functions
___

### Q: Add links to relevant protocol resources
https://docs.zivoe.com/developer-docs/core-contracts
https://docs.zivoe.com/developer-docs/lockers
___



# Audit scope


[zivoe-core-foundry @ ad27cffdf96eaaa33274bfba0dda9b60e36d29a2](https://github.com/Zivoe/zivoe-core-foundry/tree/ad27cffdf96eaaa33274bfba0dda9b60e36d29a2)
- [zivoe-core-foundry/src/ZivoeDAO.sol](zivoe-core-foundry/src/ZivoeDAO.sol)
- [zivoe-core-foundry/src/ZivoeGlobals.sol](zivoe-core-foundry/src/ZivoeGlobals.sol)
- [zivoe-core-foundry/src/ZivoeGovernorV2.sol](zivoe-core-foundry/src/ZivoeGovernorV2.sol)
- [zivoe-core-foundry/src/ZivoeITO.sol](zivoe-core-foundry/src/ZivoeITO.sol)
- [zivoe-core-foundry/src/ZivoeLocker.sol](zivoe-core-foundry/src/ZivoeLocker.sol)
- [zivoe-core-foundry/src/ZivoeMath.sol](zivoe-core-foundry/src/ZivoeMath.sol)
- [zivoe-core-foundry/src/ZivoeRewards.sol](zivoe-core-foundry/src/ZivoeRewards.sol)
- [zivoe-core-foundry/src/ZivoeRewardsVesting.sol](zivoe-core-foundry/src/ZivoeRewardsVesting.sol)
- [zivoe-core-foundry/src/ZivoeToken.sol](zivoe-core-foundry/src/ZivoeToken.sol)
- [zivoe-core-foundry/src/ZivoeTrancheToken.sol](zivoe-core-foundry/src/ZivoeTrancheToken.sol)
- [zivoe-core-foundry/src/ZivoeTranches.sol](zivoe-core-foundry/src/ZivoeTranches.sol)
- [zivoe-core-foundry/src/ZivoeYDL.sol](zivoe-core-foundry/src/ZivoeYDL.sol)
- [zivoe-core-foundry/src/libraries/FloorMath.sol](zivoe-core-foundry/src/libraries/FloorMath.sol)
- [zivoe-core-foundry/src/libraries/OwnableLocked.sol](zivoe-core-foundry/src/libraries/OwnableLocked.sol)
- [zivoe-core-foundry/src/libraries/ZivoeVotes.sol](zivoe-core-foundry/src/libraries/ZivoeVotes.sol)
- [zivoe-core-foundry/src/lockers/OCC/OCC_Modular.sol](zivoe-core-foundry/src/lockers/OCC/OCC_Modular.sol)
- [zivoe-core-foundry/src/lockers/OCE/OCE_ZVE.sol](zivoe-core-foundry/src/lockers/OCE/OCE_ZVE.sol)
- [zivoe-core-foundry/src/lockers/OCL/OCL_ZVE.sol](zivoe-core-foundry/src/lockers/OCL/OCL_ZVE.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_DAO.sol](zivoe-core-foundry/src/lockers/OCT/OCT_DAO.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_YDL.sol](zivoe-core-foundry/src/lockers/OCT/OCT_YDL.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_ZVL.sol](zivoe-core-foundry/src/lockers/OCT/OCT_ZVL.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_Convex_A.sol](zivoe-core-foundry/src/lockers/OCY/OCY_Convex_A.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_Convex_C.sol](zivoe-core-foundry/src/lockers/OCY/OCY_Convex_C.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_OUSD.sol](zivoe-core-foundry/src/lockers/OCY/OCY_OUSD.sol)
- [zivoe-core-foundry/src/lockers/Utility/ZivoeSwapper.sol](zivoe-core-foundry/src/lockers/Utility/ZivoeSwapper.sol)

[zivoe-core-testing @ 478e13327af672e7b5dfffda38b69acfed37b346](https://github.com/Zivoe/zivoe-core-testing/tree/478e13327af672e7b5dfffda38b69acfed37b346)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeDAO.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeDAO.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeGlobals.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeGlobals.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeGovernorV2.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeGovernorV2.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeITO.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeITO.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewards.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewards.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewardsVesting.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewardsVesting.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewardsVesting_Mini.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeRewardsVesting_Mini.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeSwapper.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeSwapper.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeToken.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeToken.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeTrancheToken.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeTrancheToken.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeTranches.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeTranches.sol)
- [zivoe-core-testing/src/TESTS_Core/Test_ZivoeYDL.sol](zivoe-core-testing/src/TESTS_Core/Test_ZivoeYDL.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCC_Modular.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCC_Modular.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCE_ZVE.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCE_ZVE.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCL_ZVE.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCL_ZVE.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCR_Modular.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCR_Modular.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCT_DAO.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCT_DAO.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCT_YDL.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCT_YDL.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_A.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_A.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_B.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_B.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_C.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCY_Convex_C.sol)
- [zivoe-core-testing/src/TESTS_Lockers/Test_OCY_OUSD.sol](zivoe-core-testing/src/TESTS_Lockers/Test_OCY_OUSD.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_ema.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_ema.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_juniorProportion.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_juniorProportion.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportion.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportion.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportionBase.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportionBase.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportionShortfall.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_seniorProportionShortfall.sol)
- [zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_yieldTarget.sol](zivoe-core-testing/src/TESTS_Math/Test_ZivoeMath_yieldTarget.sol)
- [zivoe-core-testing/src/TESTS_Presale/Test_ZivoePresale.sol](zivoe-core-testing/src/TESTS_Presale/Test_ZivoePresale.sol)
- [zivoe-core-testing/src/TESTS_Scenarios/Test_DeployCore.sol](zivoe-core-testing/src/TESTS_Scenarios/Test_DeployCore.sol)
- [zivoe-core-testing/src/TESTS_Scenarios/Test_ZVT.sol](zivoe-core-testing/src/TESTS_Scenarios/Test_ZVT.sol)
- [zivoe-core-testing/src/TESTS_Validation/Test_Validation_PreITO.sol](zivoe-core-testing/src/TESTS_Validation/Test_Validation_PreITO.sol)
- [zivoe-core-testing/src/Utility/Utility.sol](zivoe-core-testing/src/Utility/Utility.sol)
- [zivoe-core-testing/src/Utility/generic_tokens/ERC1155_Generic.sol](zivoe-core-testing/src/Utility/generic_tokens/ERC1155_Generic.sol)
- [zivoe-core-testing/src/Utility/generic_tokens/ERC721_Generic.sol](zivoe-core-testing/src/Utility/generic_tokens/ERC721_Generic.sol)
- [zivoe-core-testing/src/Utility/users/Admin.sol](zivoe-core-testing/src/Utility/users/Admin.sol)
- [zivoe-core-testing/src/Utility/users/Blackhat.sol](zivoe-core-testing/src/Utility/users/Blackhat.sol)
- [zivoe-core-testing/src/Utility/users/Borrower.sol](zivoe-core-testing/src/Utility/users/Borrower.sol)
- [zivoe-core-testing/src/Utility/users/Deployer.sol](zivoe-core-testing/src/Utility/users/Deployer.sol)
- [zivoe-core-testing/src/Utility/users/Investor.sol](zivoe-core-testing/src/Utility/users/Investor.sol)
- [zivoe-core-testing/src/Utility/users/Manager.sol](zivoe-core-testing/src/Utility/users/Manager.sol)
- [zivoe-core-testing/src/Utility/users/Vester.sol](zivoe-core-testing/src/Utility/users/Vester.sol)




[zivoe-core-foundry @ ad27cffdf96eaaa33274bfba0dda9b60e36d29a2](https://github.com/Zivoe/zivoe-core-foundry/tree/ad27cffdf96eaaa33274bfba0dda9b60e36d29a2)
- [zivoe-core-foundry/src/ZivoeDAO.sol](zivoe-core-foundry/src/ZivoeDAO.sol)
- [zivoe-core-foundry/src/ZivoeGlobals.sol](zivoe-core-foundry/src/ZivoeGlobals.sol)
- [zivoe-core-foundry/src/ZivoeGovernorV2.sol](zivoe-core-foundry/src/ZivoeGovernorV2.sol)
- [zivoe-core-foundry/src/ZivoeITO.sol](zivoe-core-foundry/src/ZivoeITO.sol)
- [zivoe-core-foundry/src/ZivoeLocker.sol](zivoe-core-foundry/src/ZivoeLocker.sol)
- [zivoe-core-foundry/src/ZivoeMath.sol](zivoe-core-foundry/src/ZivoeMath.sol)
- [zivoe-core-foundry/src/ZivoeRewards.sol](zivoe-core-foundry/src/ZivoeRewards.sol)
- [zivoe-core-foundry/src/ZivoeRewardsVesting.sol](zivoe-core-foundry/src/ZivoeRewardsVesting.sol)
- [zivoe-core-foundry/src/ZivoeToken.sol](zivoe-core-foundry/src/ZivoeToken.sol)
- [zivoe-core-foundry/src/ZivoeTrancheToken.sol](zivoe-core-foundry/src/ZivoeTrancheToken.sol)
- [zivoe-core-foundry/src/ZivoeTranches.sol](zivoe-core-foundry/src/ZivoeTranches.sol)
- [zivoe-core-foundry/src/ZivoeYDL.sol](zivoe-core-foundry/src/ZivoeYDL.sol)
- [zivoe-core-foundry/src/libraries/FloorMath.sol](zivoe-core-foundry/src/libraries/FloorMath.sol)
- [zivoe-core-foundry/src/libraries/OwnableLocked.sol](zivoe-core-foundry/src/libraries/OwnableLocked.sol)
- [zivoe-core-foundry/src/libraries/ZivoeVotes.sol](zivoe-core-foundry/src/libraries/ZivoeVotes.sol)
- [zivoe-core-foundry/src/lockers/OCC/OCC_Modular.sol](zivoe-core-foundry/src/lockers/OCC/OCC_Modular.sol)
- [zivoe-core-foundry/src/lockers/OCE/OCE_ZVE.sol](zivoe-core-foundry/src/lockers/OCE/OCE_ZVE.sol)
- [zivoe-core-foundry/src/lockers/OCL/OCL_ZVE.sol](zivoe-core-foundry/src/lockers/OCL/OCL_ZVE.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_DAO.sol](zivoe-core-foundry/src/lockers/OCT/OCT_DAO.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_YDL.sol](zivoe-core-foundry/src/lockers/OCT/OCT_YDL.sol)
- [zivoe-core-foundry/src/lockers/OCT/OCT_ZVL.sol](zivoe-core-foundry/src/lockers/OCT/OCT_ZVL.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_Convex_A.sol](zivoe-core-foundry/src/lockers/OCY/OCY_Convex_A.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_Convex_C.sol](zivoe-core-foundry/src/lockers/OCY/OCY_Convex_C.sol)
- [zivoe-core-foundry/src/lockers/OCY/OCY_OUSD.sol](zivoe-core-foundry/src/lockers/OCY/OCY_OUSD.sol)
- [zivoe-core-foundry/src/lockers/Utility/ZivoeSwapper.sol](zivoe-core-foundry/src/lockers/Utility/ZivoeSwapper.sol)

