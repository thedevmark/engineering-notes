# Inbound Job-Status Sync: Privacy-First Detection

Application tracking often fails when a reply arrives by email but never makes it back to the tracker. Pathos lets a candidate forward selected job-search messages to a private address. It identifies the related application, extracts a possible status change, and decides whether to apply that change or hold it for review.

This is forwarding, not a connection to the candidate's entire mailbox. The candidate chooses what enters the system.

## Authenticate before reading

The inbound Edge Function accepts a verified provider webhook or an authorized ingest request. It rejects requests without valid authentication, checks the recipient address, and resolves the private forwarding alias to the account that owns it. A paused alias does not update that account. These checks happen before a message can affect application state.

The handler uses the forwarded content during processing to identify sender, company, role, message type, and timing. It does not keep the raw body, HTML, or headers as a long-term Pathos artifact. A bounded audit record retains the evidence needed to explain a decision and support correction; the product's published retention limit for those records is up to 90 days. Email providers may have separate retention under their own terms.

## Detect the job and the status separately

The sender's domain, forwarding context, subject, message body, and known applications can all provide clues. A recruiting platform or a personal mailbox is weaker employer evidence than a verified company domain. Several open roles at one company also require role-level disambiguation. An uncertain match must not be forced onto a convenient application.

Classification starts with explicit signals for events such as an interview, rejection, or offer. Conflicting language is a reason to review, not a reason to count whichever keyword appears most often. A bounded model fallback can interpret unresolved cases, but its output still passes the same matching, confidence, and state-transition checks. When the model path is unavailable, deterministic classification and manual review remain available.

## Make the consequence reversible

A sufficiently supported, permitted status change can be applied to the tracker. Plausible but uncertain evidence is staged for the candidate. Weak or irrelevant evidence does not change the job. Guardrails prevent a later ambiguous message from overwriting a more consequential confirmed state.

The review path retains the prior status and the reason for the suggestion. The candidate can confirm, dismiss, correct, or undo an update. That makes detection useful without requiring the person to trust every automated interpretation.

The implementation lives in [Pathos](https://github.com/thedevmark/pathosapp), chiefly in its inbound Edge Function and tracker review flow. [Building Pathos](../how-i-built-pathos/) explains how this boundary fits the wider job-search system.
