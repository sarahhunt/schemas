.. _alleleAnnotations:


AlleleAnnotations API
!!!!!!!!!!!!!!!!!!!!!

See `AlleleAnnotations schema <../schemas/alleleAnnotations.html>`_ for a detailed reference.

AlleleAnnotations Data Model
@@@@@@@@@@@@@@@@@@@@@@@@@@@

Variant alleles can be annotated by comparing them to other reference data sets 
using a variety of algorithms. A standard form of annotation is to compare 
alleles to a transcript set and calculate the expected functional consequence 
of the change. 
This API supports the mining of variant annotations by region or genomic feature
and the filtering of the results by predicted functional effect.

The model has the following data types:
==================================== =======================================================================
Record	                             | Description
==================================== =======================================================================
:avro:record:`VariantAnnotationSet`  | A VariantAnnotationSet record groups VariantAnnotation records. 
                                     | It represents the comparison of a VariantSet to a specified  
                                     | reference data set using specified algorithms. It holds information 
                                     | describing the software and reference data versions use.
:avro:record:`VariantAnnotation`     | A VariantAnnotation record represents the result of comparing a 
                                     | single variant to the set of reference data. It contains 
                                     | structured sub-records and a flexible key-value pair ‘info’ field.
:avro:record:`TranscriptEffect`      | A transcript effect record describes the predicted effect of an 
                                     | allele on a transcript.
:avro:record:`AlleleLocation`        | An allele location record holds the location of an allele relative 
                                     | to a non-genomic coordinate system such as a CDS or protein. It 
                                     | holds the reference and alternate sequence where appropriate
:avro:record:`AnalysisResult`        | An AnalysisResult record holds the output of a prediction package 
                                     | such as SIFT on a specific allele.
==================================== =======================================================================

TranscriptEffect attributes

A VariantAnnotation record may have many TranscriptEffect records as one is
reported for each possible combination of alternate alleles and overlapping 
transcripts. The record includes:
*	The identifier of the transcript feature the variant was analysed against.
*	The alternate allele of the variant analysed. This is necessary as the 
        current variant model supports multiple alternate alleles.
*	The predicted effects of the allele on the transcript, which should be 
        described using Sequence Ontology terms.
*	Human Genome Variation Society variant description nomenclature at genomic 
        transcript and protein level. 
*	AlleleLocation records describing the changes at cDNA, CDS and protein level.
*	A set of results from prediction packages analyzing the allele impact.
*	A summary impact classification reflecting the highest impact consequence.

Impact Classification

The predicted impact of the allele on the transcript is summarized using the terms:
*	HIGH - the variant highly disrupts protein function
*	MODERATE - Moderately disrupts protein function
*	LOW - Low disruption of protein impact
*	MODIFIER - No known effect


