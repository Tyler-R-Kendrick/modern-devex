# Modern DevX: Optimizing Development Costs with Codespaces and Bridge to Kubernetes

To save cloud costs, you need to choose the right tools for your app needs. In this example, we will show you how to use GitHub codespaces with cloud native tools for a low-cost Kubernetes App.

## Codespaces: Accelerating Development & Reducing Costs

### What are the costs?
[link](https://docs.github.com/en/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces) 

Costs for Codespaces are determined by compute and storage as noted by the table:

| Component | Machine type | Unit of measure | Included usage multiplier | Price |
|-----------|--------------|-----------------|---------------------------|-------|
| Codespaces compute | 2 core | 1 hour | 2 | $0.18 |
| Codespaces compute | 4 core | 1 hour | 4 | $0.36 |
| Codespaces compute | 8 core | 1 hour | 8 | $0.72 |
| Codespaces compute | 16 core | 1 hour | 16 | $1.44 |
| Codespaces compute | 32 core | 1 hour | 32 | $2.88 |
| Codespaces storage | Storage | 1 GB-month | Not applicable | $0.07 |

#### Storage

The GB-month unit of storage is a time-based measurement, 1 GB-month being 1 GB of storage usage for one whole month. The disk space used by all of your codespaces and prebuilds is assessed once an hour and your current GB-month usage is recalculated. Therefore, while you have codespaces and prebuilds, your GB-month usage will increase throughout the month. For example, if the storage totals 15 GB, and remains unchanged throughout your monthly billing cycle, then you will have used 7.5 GB halfway through the month, and 15 GB at the end of the month. For more information, see "About billing for storage usage" later in this article.

To optimize storage, reduce the disk space of the Codespace instance. Unused tools in the base image, install scripts, IDE toolsets, and IDE extensions increase disk usage. So, to mitigate this, you may build your own image and push the dev tools off of the development machine.

#### Compute

A "core hour" is a measure used for included compute usage. To calculate core hours, multiply the number of hours for which a codespace has been active by the multiplier in the pricing table later in this article. For the basic machine types, the multiplier is the number of processor cores in the machine that hosts the codespace. For example, if you use a 2-core machine for your codespace and it's active for an hour, you have used 2 core hours. If you use an 8-core machine for an hour, you have used 8 core hours. If you use an 8-core machine for two hours, you have used 16 core hours.

Higher-core machines are mainly used for running and debugging applications, not for compilation. To reduce the compute needs for these scenarios, we can use a shared development cluster instead of the developer’s machine.

### Reducing Configuration Costs

Configuring your environment for development can cause significant costs in the form of development delays. In order to reduce these costs, a variety of mitigations can be made.

#### Reducing costs with prebuilt containers

[link](https://docs.github.com/en/codespaces/prebuilding-your-codespaces/about-github-codespaces-prebuilds) 

Large containers that have long startup and build times can be made more quickly available through prebuilding the image for increased storage cost.

#### Dotfiles for user settings

[link](https://dotfiles.github.io/)

Configuring user settings can that a developer is familiar with can be important to effectively developing in a timely manner. By utilizing dotfiles, developers are able to carry along their preferred user settings across development environments - allowing seemless transition when moving between project repositories.

#### Reducing compute costs with Bridge to Kubernetes.

[link](https://learn.microsoft.com/en-us/visualstudio/bridge/overview-bridge-to-kubernetes)

Cloud native environments need developers to install container tools for local development and debugging.

Bridge to Kubernetes can save storage on the codespace by using the cluster instead of the developer machine for container tools. It can also save compute when running or debugging the application, letting the developer use AKS billing on a shared cluster instead of paying more for each developer.

#### Developer Tools for Azure Kubernetes Service (AKS) & Draft

[link](https://learn.microsoft.com/en-us/azure/aks/draft)

Creating container artifacts requires a different set of skills and infrastructure knowledge than it takes to produce high quality software. By leveraging generative tools like Draft, developers can reduce time lost writing container definitions and helm charts, in favor of letting the tooling generate it.

#### Porter (CNAB)

[link](https://porter.sh/docs/learn/)

Cloud Native applications have many processes that communicate and deploy together. The services and infrastructure for these applications are often diverse and unclear.

Cloud Native Application Bundles (CNAB) simplify this problem. They standardize how to bundle and distribute these complex applications. Tools like Porter help developers deliver faster.
   
#### Azure Developer CLI

[link](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/overview)

Setting up the development workspace outside the development box is usually another impediment to developer productivity. Tools like the Azure Developer CLI let devs quickly deploy infrastructure to their own Azure subscription.

### Inner Loop Optimizations

Beyond optimizations to configuration time and outer loop concerns, Codepsaces offers many improvements to the inner loop for developers through CLI tools, extensions, and copilots.
   
#### Copilot / Intellicode

[link](https://resources.github.com/copilot-for-business/)

With Copilot, many language patterns can be completed through prompts, allowing developers to significantly improve their implementation time.

#### Language (C#) Dev Kits

[link](https://learn.microsoft.com/en-us/visualstudio/subscriptions/vs-c-sharp-dev-kit)

By utilizing language specific dev kits, developers can leverage industry standard toolsets to further reduce implementation time through a more unified development experience.

#### Azurite

[link](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azurite?tabs=visual-studio)

External services can slow down development when running and debugging the application.

Emulators and service fakes can speed up the inner loop. Azurite is a storage emulator for this purpose.

   ### Real-world examples of cost savings and improved velocity.
