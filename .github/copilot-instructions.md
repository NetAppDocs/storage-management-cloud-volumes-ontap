## Copilot instructions for Cloud Volumes ONTAP documentation

### Repository overview
Product: Cloud Volumes ONTAP

Cloud Volumes ONTAP is a software-only storage appliance that runs ONTAP in public cloud environments and is managed through the *NetApp Console*. This repository documents deployment, networking, storage, security, licensing, and operations across *AWS*, *Microsoft Azure*, and *Google Cloud*.

### Repository structure
- Primary product docs in AsciiDoc (`concept-*.adoc`, `task-*.adoc`, `reference-*.adoc`, `whats-new.adoc`, `legal-notices.adoc`)
- `_include/` – Reusable content snippets included by task and reference pages
- `_whatsnew/` – Date-stamped release-note fragments included into `whats-new.adoc`
- `media/` – Shared diagrams, screenshots, and architecture visuals referenced by docs pages
- `store-redirects/` – Redirect-only pages that map legacy permalinks to current page locations
- `.github/` – Repository metadata and Copilot-specific instruction files

### Product-specific context
**Architecture and components:**
- *Cloud Volumes ONTAP* runs as either a *single-node* system or an *HA pair*; HA uses two nodes with synchronously mirrored data and a *mediator* instance for takeover/giveback coordination.
- Deployments are created from the *NetApp Console* using a *Console agent* and are represented as Cloud Volumes ONTAP systems in the UI.
- Storage is organized as cloud provider disks grouped into *aggregates*, which host *volumes*; for iSCSI workflows, the Console creates one *LUN* per iSCSI volume.
- Data tiering uses *FabricPool* to move inactive data from a performance tier (cloud disks) to a capacity tier (object storage bucket/container), with one object-store target per system.

**Key concepts:**
- A *storage VM (SVM)* (also called a *vserver*) is the ONTAP virtual storage server that presents data services to clients.
- Supported client protocols include *NFS*, *SMB*, *iSCSI*, *NVMe-TCP*, and *S3*; protocol behavior and management capabilities differ by feature.
- Encryption combines ONTAP-native options (*NVE*/*NAE*) with cloud-provider key services, and ransomware guidance relies on *Snapshot policy* coverage and *FPolicy* controls.
- Licensing concepts center on *capacity-based licensing* packages, *Keystone Subscription* for HA pairs, and legacy *node-based* license conversion workflows.

**Naming conventions and terminology:**
- Use *NetApp Console* and *Console agent* exactly as written in this repository.
- Use *Cloud Volumes ONTAP system*, *HA pair*, *single-node*, *aggregate*, *volume*, *LUN*, and *storage VM (SVM)* consistently; these terms map to distinct resources and operations.
- Cloud-specific data-tiering terms are *Amazon S3 bucket*, *Azure Blob container*, and *Google Cloud Storage bucket*.
- Common action patterns in page names are `task-*` for procedures, `concept-*` for product behavior, and `reference-*` for limits/networking/config details.

### Typical user workflows
**Initial deployment:** Create *Console agent* → Plan cloud-specific configuration → Configure networking and encryption prerequisites → Set up licensing → Deploy Cloud Volumes ONTAP from the Console
**Storage provisioning:** Select target Cloud Volumes ONTAP system/SVM → Create aggregate or use existing capacity → Create volume with protocol and policy settings → Mount volume or connect host/LUN
**Cost optimization with tiering:** Validate object-storage/network prerequisites → Enable or edit volume tiering policy → Monitor performance/capacity tiers → Adjust storage class or access tier as needed
**Operations and protection:** Verify AutoSupport and event settings → Manage volumes/aggregates/SVMs → Configure encryption keys and ransomware controls → Upgrade or modify system settings