# SharedStringTableHandler

class SharedStringHandler extends DefaultHandler {
    private String tag;
    private List <String> values;
    private String value;

    public List <String> getValues() {
        return values;
    }

    public void startDocument() throws SAXException {
        super.startDocument();
        values = new ArrayList <String>();
    }

    @Override
    public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
        super.startElement(uri , localName, qName, attributes);
        tag = qName;
        if (qName.equals( "si" ))  {
            //When you encounter the tag si, read the data, the data will be divided into several <t></t> because of the format, and the content of all t tags in the si tag is added up to the content of a cell
            value = "";
        }
    }

    @Override
    public void endElement(String uri, String localName, String qName) throws SAXException {
        super.endElement( uri ,localName ,qName);
        tag = "";
        if (qName.equals("si")) {
            //When parsed to each When si ends the tag, add the content of the obtained t tag to the data list
            values.add(value);
}
    }

    @Override
    public void characters(char[ ] ch, int start, int length) throws SAXException {
        //The method here is to read the contents of the tag
        super.characters(ch, start, length);
        if (tag.equals("t")) {
            value = value + new String(ch, start, length);
}
    }
}
