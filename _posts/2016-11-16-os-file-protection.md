---
layout: post
title: "OS: File Protection"
date: 2016-11-16
sources: Modern Operation Systems, Tanenbaum & Bos; lecture
type: summary
---

## Policy vs Mechanism
In terms of protection, a policy defines what choices are made, while a mechanism defines how those choices are carried out. The same mechanism can be used to enforce different policy decisions.

## Protection Mechanism
A protection mechanism can enforce policies about which users have access to which resources.

When a user tries to access a resource, a protection mechanism must authenticate a user's identity, making sure that they are who they claim they are. One way to do this involves using passwords.

Once it determines a user's identity, it must figure out whether the user can access the specified resource. A protection domain defines a set of users, and a protection matrix provides the access privileges for each resource by each domain. However, since many domains do not have access to many resources, this matrix is sparse and storing the entire matrix would take up too much space. Instead, Access Control Lists or Capabilities lists can store authorization information.

With ACLs, each resource has a list containing domains and the privileges they have for that resource. However, if many domains have access to a resource, searching through the list for a specific domain could take a long time. In addition, if ACLs are only checked when a user opens a file, then changes in resources privileges might not be reflected right away. If a user opens a file, they will retain their privileges until they close the file, even if their access privileges change while they have the file open.

Instead of ACLs, capability lists can store the information in the protextion matrix. In this approach, each user has a list of resources and privileges. These lists can also become very long, and if a user has access to many resources then it could take a long time to find their access privileges for a specific resource. In addition, revoking a user's access privileges might prove difficult if each user owns their own capabilities list.

Once the computer figures out whether a user has access to a resource, it needs a way to enforce that access privilege. For instance, the kernel might have the responsibility of enforcing access privileges of user processes.
