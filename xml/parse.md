# XML parsing

`package jshint

import (
	"encoding/xml"
	"log"
)

type Checkstyle struct {
	Version string `xml:"version,attr"`
	Files   []File `xml:"file"`
}

type File struct {
	Name   string  `xml:"name,attr"`
	Errors []Error `xml:"error"`
}

type Error struct {
	Line     uint   `xml:"line,attr"`
	Column   uint   `xml:"column,attr"`
	Severity string `xml:"severity,attr"`
	Message  string `xml:"message,attr"`
}

func NewErrors(errorXml []byte) Checkstyle {
	//Example string
	//<?xml version="1.0" encoding="utf-8"?>
	//<checkstyle version="4.3">
	//  <file name="myfile.js">
	//    <error line="10" column="39" severity="error"
	//      message="Octal literals are not allowed in strict mode."/>
	//  </file>
	//</checkstyle>
	var report Checkstyle
	err := xml.Unmarshal(errorXml, &report)
	if err != nil {
		log.Fatalf("Xml parsing error: %s", err.Error())
	}

	return report
}`