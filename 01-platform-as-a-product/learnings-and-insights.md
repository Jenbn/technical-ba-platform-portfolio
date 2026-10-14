# What I Learned About Platform Teams and Product Thinking

## 1. My First Understanding of Platform Teams

My first assignment as a Business Analyst was in a platform team. Initially, I thought a platform team was primarily responsible for handling support tickets raised by stream-aligned teams: investigating what wasn't working and fixing it.

I also understood that platform teams managed underlying infrastructure and shared technical capabilities, such as databases, CI/CD pipelines, compliance requirements, security baselines, and the tools and technologies used by other stream-aligned teams.

While these responsibilities were indeed part of our work, I soon realised, thanks to my teammates and leads, that a platform team could be much more than that.

**The turning point was understanding the idea of treating the Platform as a Product.**

## 2. Discovering Platform as a Product

One of the most interesting aspects of working in a platform team was discovering how closely product thinking could be applied to internal technical services.

Our users were not external customers but colleagues working in stream-aligned teams. This gave me the opportunity to interact directly with them, understand their workflows, conduct user interviews, and learn about the challenges they faced.

Rather than relying exclusively on support tickets, we could proactively interview users, understand their pain points, collect feedback, and use metrics to evaluate our platform capabilities. These insights helped us challenge assumptions and make more informed prioritisation decisions, even when we couldn't accommodate every request.

This experience changed how I understood the role of a Business Analyst in a platform team. It wasn't simply about gathering requirements, but also about understanding the problems behind them.

## 3. Discovering the Value of Self-Service

Before joining this team, I wasn't familiar with the concept of self-service in the context of software delivery.

Our team provided capabilities that allowed developers, QAs, BAs, and other team members to perform certain activities independently, without having to raise a support ticket and wait for the platform team to handle the request. For example, workflows enabled teams to provision databases, bootstrap services in AWS, or use supported services and technologies without requiring manual intervention from our team for every request.

What previously might have required coordination, waiting time, and multiple interactions could instead be achieved through a standardised workflow.

I began to understand that the value of a platform wasn't simply in providing infrastructure or tools, but in **reducing friction and enabling other teams to focus on delivering their own products.**

### Documentation as Part of Developer Experience

One area where I was able to contribute was improving how our documentation was structured, making it easier for stream-aligned teams to distinguish between information relevant to them and internal platform-team procedures.

This helped me appreciate that developer experience isn't limited to automation and technical capabilities. Clear documentation, understandable processes, and accessible support information are equally important in making a platform usable.

## 4. Product Decisions and Trade-offs

One of my biggest learning moments was realising that a platform team doesn't necessarily need to accommodate every individual request from every stream-aligned team. Instead, the team needs to identify common needs and provide capabilities that create value across multiple consumers.

For example, if a particular technology was only required by one team, we wouldn't necessarily take responsibility for managing that technology ourselves. Our role could instead be to provide the necessary foundations, enabling that team to adopt and manage the technology independently. This might involve granting access to the required AWS capabilities or allowing the team to extend one of our supported base images.

This distinction helped me understand the importance of balancing **standardisation and flexibility**, while ensuring that responsibilities remained clear.

Another important lesson was the value of establishing and maintaining a clear responsibility model between the platform team and stream-aligned teams. We frequently received support tickets or Slack messages requesting assistance with issues that fell under the responsibility of the stream-aligned teams themselves. This highlighted the need to make ownership boundaries more transparent and accessible. By sharing the responsibility model and ensuring teams understood their areas of ownership, we reduced unnecessary support requests and improved support cycle time.

This taught me that **clearly defined and regularly maintained responsibilities go beyong setting boundaries**: they enable greater team autonomy, reduce dependencies, and allow the platform team to focus on shared capabilities.

Ultimately, I learned that effective platform product management involves not only deciding what to provide, but also defining what the platform should own, what stream-aligned teams should manage themselves, and how to enable them to do so successfully.

## 5. Challenges of Working in a Platform Team

One of the biggest challenges I experienced was coordinating changes across multiple teams. In our case, this involved working with 14 stream-aligned teams, each with its own priorities, deadlines, and dependencies.

For example, retiring a technology wasn't simply a matter of deciding to stop supporting it. We needed to consider which teams were still using it, communicate the upcoming changes, understand their dependencies, and coordinate the transition. Even when a change was technically straightforward, the organisational coordination could be challenging.

This experience helped me understand that platform product work involves more than defining features or managing a backlog. It also requires stakeholder management, dependency analysis, communication, and balancing platform-wide objectives with the priorities of consuming teams.

## 6. Why Platform Teams Interest Me

My experience in this team sparked a genuine interest in platform engineering and developer experience.

Software product discussions often focus on the end users of an application. While this is essential, I believe it's equally important to consider the people building and maintaining those applications.

Developers and other delivery team members should be able to focus on their core responsibilities rather than spending unnecessary time waiting for infrastructure changes, access requests, deployments, or support.

I find it particularly motivating to contribute to a team that helps make this possible.

As a Business Analyst with a background in Quality Analysis, I enjoy understanding how people work, identifying friction, questioning assumptions, and helping translate problems into practical improvements.

My biggest takeaway is that a successful platform is not defined only by the technologies it provides, but by how effectively it enables the teams using it.
