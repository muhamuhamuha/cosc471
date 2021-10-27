<style>

.uline {
  text-decoration: #000 wavy underline;
}

</style>

# Week 8: Relational Database Design

* Informal design guidelines
  * principles of goodness
    * each tuple should represent one entity
      * attributes of different entities  should not be mixed in the same relation
      * only foreign keys should be used to refer to other entities
      * entity and relationship attributes should be kept apart as much as possible
      * reduce null values in rows
      * lossless join decomposition
      * design a schema that does not suffer from INSERT DELETE UPDATE anomalies (redundancy)
    * Consider EMP_PROJ(<span class="uline">PKID</span>, Emp#, Proj#, Ename, Pname, No_hours)
      * DELETE ANOMALY
        * project is deleted, it will also delete all the employees associated with that project
      * INSERT ANOMALY
        * cannot insert a project if there's no employee assigned to it and vice versa
      * UPDATE ANOMALY
        * changing the name of project number P1 from 'Billing' to 'Customer-Accounting' will cause this update to be made for all 100 employees working on P1
        * representing project as its own relation means it only needs to be updated 1
      * 
    * Nulls:
      * attribute not applicable or invalid
      * attribute value unknown (may exist)
      * value known but unavailable

  * anomalies
  * lossless join decomposition
* Functional dependencies
* Normalization
  * First Normal Form
    * all attributes depend on the key
  * Second Normal Form
    * all attributes depend on the __whole key__
  * Third Normal Form
    * all attributes depend on __nothing but the key__

Conceptual -> Logical -> Physical
