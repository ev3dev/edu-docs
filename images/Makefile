DIAGRAMS='$(HOME)/node_modules/diagrams/bin/diagrams.js'

DOT_TARGETS = 	ev3dev-related-repositories.dot.svg \
		ev3dev-software-packages.dot.svg
FLOW_TARGETS = 	workflow-c-cpp.flowchart.svg

targets: $(DOT_TARGETS) $(FLOW_TARGETS)

clean:
	rm *.svg

%.dot.svg: %.dot
	$(DIAGRAMS) dot $< $@

%.flowchart.svg: %.flowchart
	$(DIAGRAMS) flowchart $< $@

