# Content Delivery Network

[Reference](https://aws.amazon.com/what-is/cdn/)

## What is CDN

A CDN is a network of servers that speed up data and application loading for users by storing copies static content closer to the users.

Instead of the origin server, the users get content from CDN servers that are geographically close to them.

> [!summary] Origin Server
> 
> The web server that hosts the application. It can be far from the actual users of the application.

^fd9128

## Benefits of CDN

- **Faster page loading** time for better user experience;
- **Reduce the bandwidth** consumed by incoming request and outgoing data at the [origin server](Content%20Delivery%20Network.md#^fd9128);
- **Increase content availability** by serving the content from CDN servers instead of the [origin server](Content%20Delivery%20Network.md#^fd9128);
- **Improve web security** by distributing incoming DDoS attacks to multiple intermediary servers.

## What does CDN deliver

> [!note] Static Content
> 
> Things that are the same for all users, such as website header images, logos, and font styles.

> [!note] Dynamic Content
> 
> Things that are unique to each user, such as social media news feeds, weather reports, login status, and chat messages. The [origin server](Content%20Delivery%20Network.md#^fd9128) must generate the content each time a user interacts with the website.

## How CDNs work

> [!summary] Point of Presence
> 
> A POP is a group of CDN edge servers at a geographical location.

^8edb67

> [!note] Caching
> 
> Caching is the act of storing copies of data at multiple servers. In a CDN, when the origin server responds to a user's request, it also sends a copy of the data to the nearest [POP](Content%20Delivery%20Network.md#^8edb67). Next time the same content is requested, the POP sends the data rather than the origin server.

> [!note] Dynamic Acceleration
> Dynamic content are not ideal for caching because they change every time. CDN servers accelerate connection between the user and the [origin server](Content%20Delivery%20Network.md#^fd9128) by several methods.
> - Intelligent routing algorithms
> - Geographic proximity to users
> - Process user requests and reduce their size
> - Trusted connection between CDN and origin server that reduces verification steps

> [!note] Edge Logic Computations
> The CDN edge servers can perform logical computations that simplify communication between the client and server. For example, this server can do the following:
> 
> - Inspect user requests and modify caching behavior;
> - Validate and handle incorrect user requests;
> - Modify or optimize content before responding.
> 
> Distribution of application logic between the web servers and the network edge helps developers offload origin servers' compute requirements and improve website performance.
