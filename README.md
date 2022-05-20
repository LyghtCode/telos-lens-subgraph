# Subgraph for Lens Protocols

-In process-

todo:

- Finish the follower
- fromProfile in Follow is not working
- Comment all the entities
- Last Dates in LensInfo
- Continue investigating about modules and how to represent them

**Link to the hosted service subgraph :**
https://thegraph.com/hosted-service/subgraph/rtomas/lens-subgraph
(there are some saved queries to play with the subgraph)

---

**Contract from the collection :**
https://polygonscan.com/address/0xDb46d1Dc155634FbC732f92E853b10B288AD5a1d

**Official Website :**
https://lens.xyz/

```mermaid
classDiagram
class LensInfo {
	ID! id
	BigInt! totalProfiles
	BigInt! totalAccounts
	BigInt! totalPosts
	BigInt! totalComments
	BigInt! totalMirror
	BigInt! totalPublications
	BigInt! totalFollowers
	BigInt lastCommentCreatedAt
	BigInt lastPostCreatedAt
	BigInt lastMirrorCreatedAt
	BigInt lastProfileCreated
}
class Profile {
	ID! id
	BigInt! profileId
	Creator! creator
	Account! owner
	Bytes followNFT
	String followNFTURI
	String handle
	String imageURI
	BigInt createdAt
	Bytes followModule
	Bytes followModuleReturnData
	Bytes dispatcher
	BigInt! lastUpdated
	[Comment!] comments
	[Post!] posts
	[Mirror!] mirrors
}
class Account {
	ID! id
	Bytes! address
	[Profile!]! profiles
}
class Creator {
	ID! id
	Bytes! address
	Boolean! isWhitelisted
	BigInt! lastUpdated
}
class Publication {
	<<interface>>
	ID! id
	Profile! fromProfile
	BigInt! pubId
	Bytes! referenceModule
	Bytes referenceModuleReturnData
	BigInt! timestamp
}
class Post {
	ID! id
	Profile! fromProfile
	BigInt! pubId
	Bytes! referenceModule
	Bytes referenceModuleReturnData
	BigInt! timestamp
	String! contentURI
	Bytes! collectModule
	Bytes collectModuleReturnData
}
class Mirror {
	ID! id
	Profile! fromProfile
	BigInt! pubId
	Bytes! referenceModule
	Bytes referenceModuleReturnData
	BigInt! timestamp
	BigInt! profileIdPointed
	BigInt! pubIdPointed
}
class Comment {
	ID! id
	Profile! fromProfile
	BigInt! pubId
	Bytes! referenceModule
	Bytes referenceModuleReturnData
	BigInt! timestamp
	String! contentURI
	BigInt! profileIdPointed
	BigInt! pubIdPointed
	Bytes collectModule
	Bytes collectModuleReturnData
}
class Follow {
	ID! id
	Account! fromProfile
	String! fromProfileAddress
	[Profile!] toProfile
	BigInt! timestamp
}
Profile --o Creator : creator
Profile --o Account : owner
Profile --o Comment : comments
Profile --o Post : posts
Profile --o Mirror : mirrors
Account --o Profile : profiles
Publication --o Profile : fromProfile
Post --o Profile : fromProfile
Publication <|-- Post
Mirror --o Profile : fromProfile
Publication <|-- Mirror
Comment --o Profile : fromProfile
Publication <|-- Comment
Follow --o Account : fromProfile
Follow --o Profile : toProfile

```
