Link Streams
^^^^^^^^^^^^
Link streams are used to define one-to-many relationships between asset elements and other asset elements, between asset elements and value streams, and between asset elements and span objects.

Link stream types must define a single Source attribute, and N Target attributes, where the source attribute represents the index of an asset element, and the target attributes represent either the indices of other asset elements or span objects, or stream IDs of associated value streams.

On-premises PI systems interpret a link object by building child AF elements beneath the Source element for each target Asset attribute, Event Frames for each target Span attribute, and PI data references for each target Value stream attribute.

AF elements can be built at the root level by sending a root link element with the Source attribute set to "_ROOT" and a Target attribute for each asset to be built at the root level.

Child elements, Event Frames, and data references cannot be built until the parent asset has been built, either via a root link, or a chain of links that resolve up to a root link.

Link streams are not presently supported in cloud-based systems.
