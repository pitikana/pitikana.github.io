# Purchase Requisition (PR) to Purchase Order (PO) Process

This document outlines the standard Procure-to-Pay (P2P) process, detailing the journey from identifying a need (PR) to paying the supplier (PO & Invoicing).

## BPMN Process Flow

```mermaid
flowchart TD
    %% Styling for BPMN elements
    classDef startEnd fill:#d4edda,stroke:#28a745,stroke-width:2px;
    classDef task fill:#f8f9fa,stroke:#343a40,stroke-width:1px;
    classDef gateway fill:#fff3cd,stroke:#ffc107,stroke-width:2px;
    
    subgraph Requester ["1. Requester / Department"]
        Start((Start)):::startEnd --> IdentifyNeed[Identify Need & Request Quote]:::task
        IdentifyNeed --> CreatePR[Create Purchase Requisition - PR]:::task
        RevisePR[Revise or Cancel PR]:::task
        ReceiveGoods[Receive Goods/Services]:::task
        CreateGR[Create Goods Receipt - GR]:::task
    end

    subgraph Approver ["2. Manager / Approver"]
        ReviewPR[Review PR against Budget]:::task
        ApprovePR{PR Approved?}:::gateway
    end

    subgraph Procurement ["3. Procurement / Purchasing"]
        Source[Source Supplier & Negotiate]:::task
        CreatePO[Create Purchase Order - PO]:::task
        SendPO[Send PO to Supplier]:::task
    end

    subgraph Supplier ["4. Supplier / Vendor"]
        ProcessOrder[Process Order]:::task
        Deliver[Deliver Goods/Services]:::task
        SendInvoice[Issue & Send Invoice]:::task
    end

    subgraph AP ["5. Accounts Payable / Finance"]
        ReceiveInvoice[Receive Invoice]:::task
        ThreeWayMatch[3-Way Match: PO + GR + Invoice]:::task
        MatchOk{Match OK?}:::gateway
        Investigate[Investigate Discrepancy]:::task
        ProcessPayment[Process Payment]:::task
        End((End)):::startEnd
    end

    %% Process Flow Connections
    CreatePR --> ReviewPR
    ReviewPR --> ApprovePR
    ApprovePR -- "Rejected" --> RevisePR
    RevisePR --> CreatePR
    ApprovePR -- "Approved" --> Source
    
    Source --> CreatePO
    CreatePO --> SendPO
    SendPO --> ProcessOrder
    
    ProcessOrder --> Deliver
    Deliver --> ReceiveGoods
    ReceiveGoods --> CreateGR
    
    Deliver --> SendInvoice
    SendInvoice --> ReceiveInvoice
    CreateGR --> ThreeWayMatch
    ReceiveInvoice --> ThreeWayMatch
    
    ThreeWayMatch --> MatchOk
    MatchOk -- "No" --> Investigate
    Investigate --> ThreeWayMatch
    MatchOk -- "Yes" --> ProcessPayment
    ProcessPayment --> End
