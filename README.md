# ptvs-rfc-002-apris-circuit-breakers
APRIS: Day-2 Operational Resilience Module for PTVS. Parametric Circuit Breakers, Automated Yield Gating, and PIPC Insurance Integration under MiCA Art. 58 and BCBS SCO60.
# PTVS-RFC-002: APRIS Parametric Circuit Breakers & Automated Yield Gating

![Status](https://img.shields.io/badge/Status-Draft%20Standard-gold)
![License](https://img.shields.io/badge/License-CC%20BY--ND%204.0-blue)
![Dependency](https://img.shields.io/badge/Dependency-PTVS--RFC--001-navy)
![DOI](https://img.shields.io/badge/DOI-10.5281/zenodo.21719175-navy)

**Version:** 1.0.0 (October 2026)  
**Author:** D. Aurelio Tamarit Blay, Forensics Oracle Initiative (PFOI)  
**Governance:** PropTrust Association (Zug, Switzerland)  
**Canonical Reference:** *Corpus Legislativum PTVS v1.0, Liber VI (APRIS)* (DOI: 10.5281/zenodo.21719175)

---

## 📋 Abstract

While **PTVS-RFC-001** establishes the initial cryptographic anchoring of physical reality (Day-0 verification), **PTVS-RFC-002** defines the **Actuarial Parametric Resolution & Insurance System (APRIS)** — the Day-2 operational resilience module of the Prop Trust Verified Standard.

APRIS provides the deterministic, smart-contract-enforced responses to continuous physical degradation, registry divergence, or operator failure. It delivers:

- **Trading Circuit Breakers** that halt secondary market transfers upon verified physical pathology
- **Automated Yield Gating** that redirects distributions to maintenance escrows upon PRRB downgrade
- **Atomic Capex Escrow Release** for emergency repairs certified by PTCEs
- **Integration with Parametric Physical Integrity Cover (PIPC)** for automated insurance payouts
- **Atomic Receiver Protocol** invocation for bankruptcy-remote protection

This specification directly addresses the operational resilience mandates of **MiCA Art. 58**, the prudential treatment requirements of **BCBS SCO60**, and the custody obligations of **ADGM Digital Asset Rules**.

---

## 🎯 Core Philosophy: Autonomous Risk Containment

APRIS operates on the principle of **Forensic Primacy**: when a Prop Trust Certified Expert (PTCE) verifies a critical physical pathology or registry divergence, the smart contract must react deterministically — removing human discretion and preventing secondary market contagion.

**The code is the law, and the law contains the risk first.**

---

## 🔗 Dependency on PTVS-RFC-001

This specification **extends** (does not replace) the `IPTVSClaimInjector` interface defined in RFC-001. Any platform implementing APRIS must first implement RFC-001.


┌─────────────────────────────────────────────────────────┐
│ PTVS-RFC-001: Physical Oracle Interface (Day-0) │
│ • QFER Injection │
│ • LO-PR Registry Anchoring │
│ • eIDAS 2.0 QES Validation │
└─────────────────────────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ PTVS-RFC-002: APRIS Module (Day-2) │
│ • Parametric Trigger Events (PTEs) │
│ • Trading Circuit Breakers │
│ • Automated Yield Gating │
│ • Atomic Capex Escrow Release │
│ • Atomic Receiver Protocol │
│ • PIPC Insurance Integration │
└─────────────────────────────────────────────────────────┘



---

## ⚡ Parametric Trigger Events (PTEs)

The APRIS module monitors for specific, predefined forensic conditions. Upon validation by a quorum of PTCEs (or a single PTCE with elevated PRRB authority), the following triggers are activated:

| PTE Code | Trigger Condition | APRIS Response | MiCA Reference |
| :--- | :--- | :--- | :--- |
| **PTE-1** | Structural Collapse / Critical Pathology | Immediate `ForensicFreezeTriggered`. Secondary transfers halted. | Art. 58 (Operational Resilience) |
| **PTE-2** | PRRB Downgrade to Speculative (BB or below) | `YieldRatingAdjusted`. Distributions gated to maintenance escrow. | Art. 36.8 (Reserve Sufficiency) |
| **PTE-3** | Registry Divergence / Double Pledge Detected | Immediate freeze + `AtomicReceiver` invocation. | Art. 46 (Custody & Segregation) |
| **PTE-4** | Telemetry Loss > 72h (Vector V5 break) | Automatic PRRB downgrade + mandatory re-inspection. | Art. 58 (Business Continuity) |
| **PTE-5** | Operator Control Loss / Obstruction | `AtomicReceiver` step-in after 30 days. | CL-PTVS IV.4 |

See [`docs/parametric-triggers.md`](./docs/parametric-triggers.md) for the full technical specification of each PTE.

---

## 💻 Smart Contract Interface (Solidity)

The core Solidity interface is located in [`/contracts/IAPRISController.sol`](./contracts/IAPRISController.sol). It is designed to be implemented by RWA issuance platforms and token contracts to react dynamically to physical pathology.

### Key Functions:

```solidity
// Gates yield and redirects to maintenance escrow
function executeYieldGating(
    bytes32 _assetId,
    uint256 _newYieldBps,
    address _escrowTarget
) external;

// Releases escrowed funds for urgent repairs (with atomic fee deduction)
function executeCapexRelease(
    bytes32 _assetId,
    uint256 _releaseAmount,
    bytes calldata _ptceSignature
) external;

// Invokes bankruptcy-remote receiver
function invokeAtomicReceiver(
    bytes32 _assetId,
    address _receiverAddress
) external;


 Compliance Mapping
Regulation
Requirement
APRIS Implementation
MiCA (EU) Art. 58
Operational resilience & business continuity
Automated ForensicFreeze prevents trading of compromised assets
MiCA (EU) Art. 36.8
Sufficient reserve assets at all times
YieldGating redirects distributions to maintenance escrow
MiCA (EU) Art. 46
Custody and segregation of reserve assets
AtomicReceiver ensures bankruptcy remoteness
BCBS SCO60
Prudential treatment of crypto exposures
Continuous PRRB rating enables Group 1a classification
ADGM COBS 7.6
Custody of client digital assets
LO-PR Registry + QFER pack provides continuous proof
eIDAS 2.0
Non-repudiation of automated actions
All APRIS triggers require valid PTCE QES signature hash
MAS Project Guardian
Trust architecture & risk management
Deterministic containment removes operator discretion


🔬 Ontology & Semantic Interoperability
The APRIS ontology (JSON-LD) is defined in /ontology/apris-schema.json. It extends the base PTVS ontology with:
ptvs:parametricTriggerEvent (PTE classification)
ptvs:circuitBreakerStatus (Active / ForensicFreezeTriggered / YieldGated / CapexEscrowReleased)
ptvs:atomicReceiverInvocation (Bankruptcy-remote step-in events)
ptvs:pipcPolicyReference (Link to parametric insurance policy)
This ontology is designed for integration with regulatory knowledge graphs (BCE, BIS, MAS) and Linked Open Vocabularies (LOV).
🔒 Security & Audit Considerations
Implementations of this interface must ensure:
PTCE Quorum Validation: Critical triggers (PTE-1, PTE-3) require multi-signature validation from registered PTCEs.
Reentrancy Protection: All functions must use the nonReentrant modifier (already included in the reference implementation).
Signature Verification: The _ptceSignature must be verified against the PTCE's eIDAS 2.0 QES certificate fingerprint via ECDSA.
Rate Limiting: executeCapexRelease must enforce a 72-hour cooldown between releases for the same asset.
Emergency Pause: A governance-controlled emergencyPause() function must be available for system-wide halt.
📚 References
Tamarit Blay, A. (2026). Corpus Legislativum PTVS v1.0. PropTrust Association. DOI: 10.5281/zenodo.21719175
Tamarit Blay, A. (2026). PTVS-RFC-001: Physical Oracle Interface. Forensics Oracle Initiative.
European Parliament. (2023). Regulation (EU) 2023/1114 (MiCA).
Basel Committee. (2022). Prudential treatment of cryptoasset exposures (SCO60).
Abu Dhabi Global Market. (2022). Digital Asset Regulations and Rules.
Monetary Authority of Singapore. (2023). Project Guardian Policy Toolkit.
📄 License

This repository, including all specifications, ontologies, and smart contract interfaces, is licensed under the **Business Source License 1.1 (BSL 1.1)**. 

This license permits non-commercial academic research, testing, and commercial use ONLY for projects with a Total Value Locked (TVL) or appraised RWA value strictly under $5,000,000 USD. Any commercial production use exceeding this threshold requires a separate commercial license from Aurema Group LLC. 

On October 22, 2029, this code will automatically transition to the MIT License.

See the `LICENSE` file in the root of this repository for the full legal text.

*VERITAS IN RE · CERTITUDO IN CODE · HONOR IN AETERNUM*



---

### 💻 ARCHIVO 2: `contracts/IAPRISController.sol`

```solidity
// SPDX-License-Identifier: BSL-1.1
pragma solidity ^0.8.20;

import "./IPTVSClaimInjector.sol";

/**
 * @title IAPRISController
 * @author Forensics Oracle Initiative (PFOI)
 * @notice Interface for the Actuarial Parametric Resolution & Insurance System (APRIS).
 * @dev Executes deterministic financial and operational containment upon verified physical pathology.
 *      Extends IPTVSClaimInjector (RFC-001) to handle Day-2 resilience.
 *      Complies with MiCA Art. 58, BCBS SCO60, and CL-PTVS Liber VI.
 */
interface IAPRISController is IPTVSClaimInjector {

    // ============ EVENTS ============

    /// @notice Emitted when yield distribution is gated due to PRRB downgrade.
    /// @param assetId The unique identifier of the tokenized RWA.
    /// @param oldYieldBps The previous yield in basis points.
    /// @param newYieldBps The new, restricted yield in basis points.
    /// @param escrowTarget The address of the maintenance escrow receiving redirected funds.
    event YieldRatingAdjusted(
        bytes32 indexed assetId,
        uint256 oldYieldBps,
        uint256 newYieldBps,
        address indexed escrowTarget
    );

    /// @notice Emitted when escrowed funds are released for emergency repairs.
    /// @param assetId The unique identifier of the tokenized RWA.
    /// @param releaseAmount The gross amount released from escrow.
    /// @param infrastructureFee The fee deducted for the PTVS infrastructure.
    /// @param netBeneficiaryAmount The net amount transferred to the repair beneficiary.
    /// @param ptceAddress The PTCE who certified the repair.
    event CapexEscrowReleased(
        bytes32 indexed assetId,
        uint256 releaseAmount,
        uint256 infrastructureFee,
        uint256 netBeneficiaryAmount,
        address indexed ptceAddress
    );

    /// @notice Emitted when the Atomic Receiver Protocol is invoked.
    /// @param assetId The unique identifier of the tokenized RWA.
    /// @param receiverAddress The designated bankruptcy-remote receiver.
    /// @param triggerReason The PTE code that triggered the invocation.
    event AtomicReceiverInvoked(
        bytes32 indexed assetId,
        address indexed receiverAddress,
        string triggerReason
    );

    /// @notice Emitted when a PIPC insurance payout is triggered.
    /// @param assetId The unique identifier of the tokenized RWA.
    /// @param payoutAmount The amount paid out by the parametric insurance.
    /// @param beneficiary The recipient of the payout.
    /// @param pteCode The Parametric Trigger Event that activated the policy.
    event PIPCPayoutExecuted(
        bytes32 indexed assetId,
        uint256 payoutAmount,
        address indexed beneficiary,
        string pteCode
    );

    // ============ FUNCTIONS ============

    /**
     * @notice Gates yield distribution and redirects funds to a maintenance escrow upon PRRB downgrade.
     * @dev Triggered by PTE-2 (Rating Downgrade to Speculative).
     * @param _assetId The ID of the RWA.
     * @param _newYieldBps The new, restricted yield in basis points.
     * @param _escrowTarget The address of the authorized Capex Escrow contract.
     */
    function executeYieldGating(
        bytes32 _assetId,
        uint256 _newYieldBps,
        address _escrowTarget
    ) external;

    /**
     * @notice Automatically releases escrowed funds for urgent repairs upon PTCE certification.
     * @dev Deducts the PTVS infrastructure fee atomically before routing to beneficiary.
     *      Enforces 72-hour cooldown between releases for the same asset.
     * @param _assetId The ID of the RWA.
     * @param _releaseAmount The gross amount to release.
     * @param _ptceSignature Cryptographic proof of the repair certification (eIDAS 2.0 QES).
     */
    function executeCapexRelease(
        bytes32 _assetId,
        uint256 _releaseAmount,
        bytes calldata _ptceSignature
    ) external;

    /**
     * @notice Triggers the Atomic Receiver Protocol in case of severe physical loss or fraud.
     * @dev Invoked by PTE-3 (Registry Divergence) or PTE-5 (Operator Control Loss).
     * @param _assetId The ID of the RWA.
     * @param _receiverAddress The designated bankruptcy-remote receiver address.
     */
    function invokeAtomicReceiver(
        bytes32 _assetId,
        address _receiverAddress
    ) external;

    /**
     * @notice Executes a parametric insurance payout upon verified PTE.
     * @dev Integrates with PIPC (Physical Integrity Parametric Cover) smart contract.
     * @param _assetId The ID of the RWA.
     * @param _payoutAmount The amount to be paid out.
     * @param _beneficiary The recipient of the payout.
     * @param _pteCode The Parametric Trigger Event code.
     */
    function executePIPCPayout(
        bytes32 _assetId,
        uint256 _payoutAmount,
        address _beneficiary,
        string calldata _pteCode
    ) external;

    /**
     * @notice Returns the current circuit breaker status of an asset.
     * @param _assetId The ID of the RWA.
     * @return status The current status (Active, ForensicFreezeTriggered, YieldGated, CapexEscrowReleased).
     */
    function getCircuitBreakerStatus(
        bytes32 _assetId
    ) external view returns (string memory status);

    /**
     * @notice Returns the timestamp of the last Capex Escrow release for an asset.
     * @param _assetId The ID of the RWA.
     * @return timestamp The Unix timestamp of the last release.
     */
    function getLastCapexReleaseTimestamp(
        bytes32 _assetId
    ) external view returns (uint256 timestamp);
}
