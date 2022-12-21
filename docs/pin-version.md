<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/reference-architecture/blob/master/docs/pin-version.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Pin Blueprint Versions

Since blueprints are managed by bundler and a Gemfile, they are natually pinned down to a version by Gemfile.lock. To update a blueprint version, you use `bundler update BLUEPRINT`. Example:

	bundle update ecs-spot

You can also pin blueprints with specific git tags, shas, or branches.  Here's an example Gemfile:

```ruby
def blueprint(name, options={})
  options = {git: "git@github.com:boltopspro/#{name}.git"}.merge!(default)
  gem(name, options)
end

blueprint "vpc", tag: "v0.1.0"
blueprint "vpc-peer", ref: "79ffcf"
blueprint "ecs-asg", branch: "master"
blueprint "ecs-spot"
```

Blueprints are tested as part of the Reference Architecture Acceptance Pipeline. The Reference Architecture with CodePipeline and CodeBuild on a daily basis with **live** resources against the master branches.  So the blueprints master branches should work just fine.
